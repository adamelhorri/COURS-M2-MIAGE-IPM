---
tags:
  - BigData
---

# TP Spark – Premières manipulations

## Environnement

- **Spark version** : 3.1.2
    
- **Scala version** : 2.12.10
    
- **Java version** : 1.8.0_232
    
- **Cluster Hadoop** : HDFS sur Docker
    

---

## 1️⃣ Afficher un message

```scala
scala> println("Bonjour à tous !")
```

**Résultat :**

```
Bonjour à tous !
```

**Explication :**

- `println` est une fonction Scala standard pour afficher du texte dans le terminal.
    
- Cette étape permet de **vérifier que Spark Shell fonctionne correctement**.
    

---

## 2️⃣ Charger le répertoire “gutenberg” dans un RDD

```scala
scala> val rdd_gut = sc.textFile("hdfs://namenode:9000/user/root/gutenberg")
```

**Résultat :**

```
rdd_gut: org.apache.spark.rdd.RDD[String] = hdfs://namenode:9000/user/root/gutenberg MapPartitionsRDD[1] at textFile at <console>:24
```

**Explication :**

- `sc.textFile()` lit un fichier ou un répertoire dans HDFS.
    
- Chaque ligne du fichier devient un élément du RDD `rdd_gut`.
    
- `RDD[String]` signifie que chaque élément est une chaîne de caractères.
    

---

## 3️⃣ Compter le nombre de lignes

```scala
scala> val nbLignes = rdd_gut.count()
scala> println(nbLignes)
```

**Résultat :**

```
147838
```

**Explication :**

- `count()` est une **action Spark** qui retourne le nombre total d’éléments du RDD.
    
- Ici, cela donne **le nombre total de lignes du corpus**.
    

---

## 4️⃣ Afficher les 3 premières lignes

```scala
scala> rdd_gut.take(3).foreach(println)
```

**Résultat :**

```
Project Gutenberg?s The Complete Works of William Shakespeare, by
William Shakespeare
```

**Explication :**

- `take(3)` : action qui récupère les **3 premiers éléments** du RDD.
    
- `foreach(println)` : affiche chaque élément.
    
- Utile pour **vérifier le contenu des données**.
    

---

## 5️⃣ Filtrer les lignes contenant le mot `"murderer"` et les compter

```scala
scala> val rdd_murderer = rdd_gut.filter(line => line.toLowerCase.contains("murderer"))
scala> val nbMurderer = rdd_murderer.count()
scala> println(nbMurderer)
```

**Résultat :**

```
119
```

**Explication :**

- `filter()` : transformation qui **conserve uniquement les lignes correspondant à une condition**.
    
- `toLowerCase` permet d’éviter les problèmes de majuscules/minuscules.
    
- `contains("murderer")` cherche le mot "murderer" dans chaque ligne.
    
- `count()` : action pour **compter le nombre de lignes filtrées**.
    

---

## 6️⃣ Calculer le nombre total de caractères

```scala
scala> val nbCaracteres = rdd_gut.map(line => line.length).reduce(_ + _)
scala> println(nbCaracteres)
```

**Résultat :**

```
5545144
```

**Explication :**

- `map(line => line.length)` : transforme chaque ligne en **nombre de caractères**.
    
- `reduce(_ + _)` : somme toutes les longueurs pour obtenir le **nombre total de caractères du corpus**.
    

---

✅ Avec ces étapes, le **TP 3 – Exo 1 est entièrement résolu** :

- RDD créé et inspecté
    
- Nombre de lignes, premières lignes, lignes filtrées et total de caractères calculés
    
