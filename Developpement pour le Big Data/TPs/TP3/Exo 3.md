---
tags:
  - BigData
---
# TP Spark – Exo 3 : WordCount amélioré (nettoyage du texte)

## Environnement

- **Spark version** : 3.1.2
    
- **Scala version** : 2.12.10
    
- **Java version** : 1.8.0_232
    
- **Cluster Hadoop** : HDFS sur Docker
    

---

## 1️⃣ Nettoyer chaque ligne

### Code Scala

```scala
val cleaned_rdd = rdd_gut.map(line =>
  line
    .replaceAll("\\[.*?\\]", "")             // Supprime tout ce qui est entre crochets []
    .replaceAll("\\b(Page|Act|Scene)\\b", "") // Supprime les mots "Page", "Act", "Scene"
    .replaceAll("\\d+", "")                    // Supprime tous les nombres
)
cleaned_rdd.take(5).foreach(println)
```

### Explication

- **`replaceAll("\\[.*?\\]", "")`** : supprime les instructions de mise en scène `[Enter Hamlet]`.
    
- **`replaceAll("\\b(Page|Act|Scene)\\b", "")`** : supprime les mots exacts “Page”, “Act” ou “Scene”.
    
- **`replaceAll("\\d+", "")`** : supprime tous les chiffres (numéros de pages, scènes, actes).
    
- `take(5).foreach(println)` permet de **vérifier le texte nettoyé**.
    

**Exemple de sortie :**

```
Project Gutenberg?s The Complete Works of William Shakespeare, by
William Shakespeare

This eBook is for the use of anyone anywhere in the United States and
```

---

## 2️⃣ Séparer chaque ligne en mots (`flatMap`)

### Code Scala

```scala
val rdd_words = cleaned_rdd.flatMap(line => line.split("\\W+"))
rdd_words.take(10).foreach(println)
```

**Explication**

- `flatMap` transforme **chaque ligne en plusieurs mots**.
    
- `split("\\W+")` découpe la ligne sur **tout caractère non alphanumérique**.
    
- Résultat : un **RDD[String]** contenant tous les mots du texte nettoyé.
    

---

## 3️⃣ Créer des couples `(mot, 1)` (`map`)

### Code Scala

```scala
val rdd_pairs = rdd_words.map(word => (word.toLowerCase, 1))
rdd_pairs.take(10).foreach(println)
```

**Explication**

- `map` transforme chaque mot en **tuple `(mot, 1)`**.
    
- `toLowerCase` uniformise les mots (pas de doublons “The” vs “the”).
    
- Résultat : un **RDD[(String, Int)]**.
    

**Exemple de sortie :**

```
("project", 1)
("gutenberg", 1)
("s", 1)
("the", 1)
("complete", 1)
...
```

---

## 4️⃣ Somme des occurrences par mot (`reduceByKey`)

### Code Scala

```scala
val rdd_counts = rdd_pairs.reduceByKey(_ + _)
rdd_counts.take(10).foreach(println)
```

**Explication**

- `reduceByKey(_ + _)` : regroupe les valeurs par mot et somme les occurrences.
    
- Résultat : un **RDD[(String, Int)]** avec le nombre d’apparitions de chaque mot.
    

**Exemple de sortie :**

```
("project", 3)
("gutenberg", 7)
("s", 15)
("the", 1234)
("complete", 5)
...
```

---

## 5️⃣ Trier par fréquence décroissante et afficher les mots les plus fréquents

### Code Scala

```scala
rdd_counts.sortBy(_._2, ascending = false).take(10).foreach(println)
```

**Explication**

- `sortBy(_._2, ascending = false)` : trie par **nombre d’occurrences**.
    
- `take(10)` : récupère les 10 mots les plus fréquents.
    
- `foreach(println)` : affiche les résultats.
    

**Exemple de sortie :**

```
("the", 1230)
("and", 980)
("i", 875)
("to", 760)
("of", 650)
("a", 540)
("you", 430)
("my", 320)
("in", 210)
("that", 200)
```

---

## 6️⃣ Version compacte – WordCount nettoyé en une seule ligne

```scala
rdd_gut
  .map(line => line.replaceAll("\\[.*?\\]", "")
                   .replaceAll("\\b(Page|Act|Scene)\\b", "")
                   .replaceAll("\\d+", ""))
  .flatMap(line => line.split("\\W+"))
  .map(word => (word.toLowerCase, 1))
  .reduceByKey(_ + _)
  .sortBy(_._2, ascending = false)
  .take(10)
  .foreach(println)
```

**Explication rapide**

- Tout le pipeline en **une seule commande** : nettoyage + WordCount + tri + affichage.
    
- Pratique pour **spark-shell ou scripts Spark rapides**.
    
