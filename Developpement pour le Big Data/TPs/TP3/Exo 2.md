---
tags:
  - BigData
---

# TP Spark – WordCount étape par étape

## Environnement

- **Spark version** : 3.1.2
    
- **Scala version** : 2.12.10
    
- **Java version** : 1.8.0_232
    
- **Cluster Hadoop** : HDFS sur Docker
    

---

## 1️⃣ Séparer chaque ligne en mots (`flatMap`)

### Code Scala

```scala
val rdd_words = rdd_gut.flatMap(line => line.split("\\W+"))
rdd_words.take(10).foreach(println)
```

**Explication :**

- `flatMap` transforme **chaque ligne** en plusieurs éléments (mots).
    
- `line.split("\\W+")` : découpe la ligne sur tout caractère **non alphanumérique**.
    
- Résultat : un **RDD[String]** contenant tous les mots.
    
- `take(10)` permet de **visualiser les 10 premiers mots**.
    

**Exemple de sortie :**

```
Project
Gutenberg
s
The
Complete
Works
...
```

---

## 2️⃣ Créer des couples clé-valeur `(mot, 1)` (`map`)

### Code Scala

```scala
val rdd_pairs = rdd_words.map(word => (word.toLowerCase, 1))
rdd_pairs.take(10).foreach(println)
```

**Explication :**

- `map` transforme chaque mot en un **tuple (clé, valeur)**.
    
    - Clé = mot
        
    - Valeur = 1
        
- `toLowerCase` uniformise les mots et évite les doublons “The” vs “the”.
    
- Résultat : un **RDD[(String, Int)]** prêt pour le comptage.
    

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

## 3️⃣ Somme des valeurs pour chaque mot (`reduceByKey`)

### Code Scala

```scala
val rdd_counts = rdd_pairs.reduceByKey(_ + _)
rdd_counts.take(10).foreach(println)
```

**Explication :**

- `reduceByKey(_ + _)` : regroupe les valeurs par **clé** et somme les occurrences.
    
- Résultat : un **RDD[(String, Int)]** contenant **chaque mot et son nombre d’occurrences**.
    
- `take(10)` permet de **vérifier les 10 premiers résultats**.
    

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

## 4️⃣ (Optionnel) Trier les mots par fréquence

```scala
rdd_counts.sortBy(_._2, ascending = false).take(10).foreach(println)
```

**Explication :**

- `sortBy(_._2, ascending = false)` : trie par la **valeur du tuple** (le nombre d’occurrences).
    
- Affiche les **10 mots les plus fréquents**.
    

---

## ✅ Résumé du pipeline WordCount

|Étape|Transformation Spark|Résultat|
|---|---|---|
|1|`flatMap(line => line.split("\\W+"))`|RDD de tous les mots|
|2|`map(word => (word.toLowerCase, 1))`|RDD de couples (mot,1)|
|3|`reduceByKey(_ + _)`|RDD de couples (mot, nb_occurrences)|
|4|`sortBy(_._2, false)` (optionnel)|Tri par fréquence|

---

💡 **Conseils pour TP / exploration**

- Toujours visualiser les RDD avec `take(n).foreach(println)` pour comprendre le résultat.
    
- Chaque transformation **ne déclenche pas le calcul**. Les actions (`count`, `collect`, `take`) **déclenchent réellement l’exécution**.
    
