---
tags:
  - BigData
---

# Rapport d'implémentation Spark : Analyse de Textes et Logs

Ce document explique le fonctionnement de trois algorithmes développés en Scala avec Apache Spark : la recherche d'anagrammes, l'analyse temporelle de logs et l'indexation de mots.

---

## 1. Recherche d'Anagrammes

**Objectif :** Identifier les mots d'un texte qui possèdent les mêmes lettres et enregistrer les groupes d'anagrammes sur HDFS.

### Le Code

Scala

```scala
val output = sc.textFile("hdfs://namenode:9000/user/root/gutenberg")
   .flatMap(_.split("\\W+"))                 // Découpage en mots
   .map(_.toLowerCase)                       // Normalisation
   .filter(w => w.matches("[a-z]+") && w.length > 1) // Nettoyage
   .distinct()                               // Suppression des doublons
   .map(w => (w.sorted, w))                  // Clé : lettres triées, Valeur : mot original
   .groupByKey()                             // Regroupement par clé (anagrammes)
   .filter(_._2.size > 1)                    // On ne garde que les vrais anagrammes
   .map { case (lettres, mots) => s"$lettres -> ${mots.mkString(", ")}" }

output.saveAsTextFile("hdfs://namenode:9000/user/root/anagrammes_final_ok")
```

### Explication Logique

- **Signature numérique** : L'astuce consiste à utiliser `w.sorted` comme clé. Par exemple, "bury" et "ruby" deviennent tous deux "bruy" une fois triés.
    
- **Transformation Map** : Chaque mot devient un couple `(alphabet_trié, mot_original)`.
    
- **Réduction Groupée** : `groupByKey()` rassemble tous les mots ayant la même signature.
    
- **Résultat** : On obtient une liste comme `bruy -> bury, ruby`.
    

---

## 2. Analyse de Hits par Quart d'Heure

**Objectif :** Compter le nombre de requêtes dans un fichier de logs pour chaque tranche de 15 minutes, uniquement entre 10h30 et 23h15.

### Le Code

Scala

```scala
val finalResult = mockData.flatMap(line => {
  val pattern = "(\\d{2}):(\\d{2}):(\\d{2})".r
  pattern.findFirstMatchIn(line).flatMap(m => {
    val h = m.group(1).toInt
    val mins = m.group(2).toInt
    val totalMins = h * 60 + mins
    
    // Filtrage temporel (10h30 à 23h15)
    if (totalMins >= 630 && totalMins <= 1395) {
      val q_min = (mins / 15) * 15            // Arrondi au quart d'heure
      Some((f"$h%02d:$q_min%02d", 1))
    } else None
  })
}).reduceByKey(_ + _).sortByKey()
```

### Explication Logique

- **Extraction & Filtrage** : On utilise une expression régulière pour extraire l'heure. On convertit tout en minutes pour faciliter le calcul des bornes.
    
- **Windowing (Fenêtrage)** : L'opération `(mins / 15) * 15` crée des "seaux" (buckets). Les minutes 00 à 14 tombent dans "00", 15 à 29 dans "15", etc.
    
- **Aggregation** : `reduceByKey(_ + _)` additionne tous les "1" pour chaque créneau horaire.
    

---

## 3. Indexation d'un mot (Index Inversé)

**Objectif :** Créer un index indiquant dans quels documents un mot spécifique apparaît.

### Le Code

Scala

```scala
val wordToFind = "spark"
val index = docs.
  flatMap { case (fileName, content) => 
    content.split("\\W+").map(word => (word.toLowerCase, fileName)) 
  }.
  filter { case (word, fileName) => word == wordToFind.toLowerCase }.
  groupByKey().
  mapValues(_.toSet.mkString(", "))
```

### Explication Logique

- **Mapping Document/Mot** : On transforme chaque document en une multitude de paires `(mot, nom_du_fichier)`.
    
- **Filtrage** : On ne conserve que les paires où le mot correspond au paramètre recherché.
    
- **Collecte** : `groupByKey()` regroupe toutes les localisations (fichiers) pour ce mot.
    
- **Nettoyage** : `toSet` garantit que si un mot apparaît plusieurs fois dans le même fichier, le nom du fichier ne sera cité qu'une seule fois.
    

---

### Résumé des concepts Spark utilisés

|**Fonction**|**Usage dans vos codes**|
|---|---|
|**flatMap**|Découper des lignes en mots ou filtrer/transformer des logs.|
|**map**|Transformer un mot en clé de tri ou formater l'affichage.|
|**reduceByKey**|Compter efficacement des occurrences (hits).|
|**groupByKey**|Rassembler des listes d'éléments (mots anagrammes, noms de fichiers).|
|**saveAsTextFile**|Ecriture durable des résultats sur le cluster HDFS.|

---

Souhaitez-vous que je génère un script automatisé pour exécuter ces trois tâches à la suite sur vos vrais fichiers HDFS ?