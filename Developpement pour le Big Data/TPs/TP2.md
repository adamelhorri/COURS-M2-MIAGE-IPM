---
tags:
  - BigData
---
# Exercice 1 : WordCount

## **Objectif**

Réaliser un job **MapReduce** sur Hadoop pour compter le nombre d’occurrences de chaque mot dans l’œuvre de Shakespeare.

---

## **Étapes détaillées**

### **1️⃣ Préparer HDFS**

1. Lancer le conteneur Hadoop (`namenode`) via Docker.
    
2. Créer le répertoire pour stocker le fichier source dans HDFS :
    

```bash
hadoop fs -mkdir -p /user/root/gutenberg
```

3. Copier le fichier source `Shakespeare.txt` depuis Windows vers le conteneur Docker :
    

```powershell
docker cp Shakespeare.txt namenode:/root/
```

4. Copier le fichier depuis le conteneur vers HDFS :
    

```bash
hadoop fs -put /root/Shakespeare.txt /user/root/gutenberg/
```

✅ Vérification :

```bash
hadoop fs -ls /user/root/gutenberg
```

> Résultat attendu : `Shakespeare.txt` présent dans HDFS.

---

### **2️⃣ Préparer le projet Java MapReduce**

1. Créer un dossier `wc` contenant 3 fichiers Java :
    
    - `WcDriver.java` → classe Driver pour configurer et lancer le job
        
    - `WcMapper.java` → Mapper qui découpe les lignes en mots
        
    - `WcReducer.java` → Reducer qui compte les occurrences par mot
        
2. Exemple de code **WcMapper.java** :
    

```java
package wc;

import java.io.IOException;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;

public class WcMapper extends Mapper<LongWritable, Text, Text, IntWritable> {
    public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
        String line = value.toString();
        for (String word : line.split("\\W+"))
            if (word.length() > 0)
                context.write(new Text(word), new IntWritable(1));
    }
}
```

---

### **3️⃣ Compiler les fichiers Java pour Java 8**

> Important : Hadoop du conteneur utilise **Java 8**, donc il faut compiler avec `-source 1.8 -target 1.8` :

```powershell
javac -source 1.8 -target 1.8 -cp ".;hadoop-common-3.2.1.jar;hadoop-mapreduce-client-core-3.2.1.jar" wc\*.java
```

✅ Vérification : chaque `.class` doit être créé dans le dossier `wc/`.

---

### **4️⃣ Créer le jar**

```powershell
jar cvf wc.jar -C . wc
```

✅ Vérification :

```powershell
jar tf wc.jar
```

> Résultat attendu :

```
wc/WcDriver.class
wc/WcMapper.class
wc/WcReducer.class
META-INF/MANIFEST.MF
```

---

### **5️⃣ Copier le jar dans le conteneur**

```powershell
docker cp wc.jar namenode:/root/
```

---

### **6️⃣ Lancer le job Hadoop WordCount**

Dans le conteneur Docker :

```bash
hadoop jar /root/wc.jar wc.WcDriver /user/root/gutenberg /user/root/wordcounts
```

💡 **Explications des paramètres** :

- `/root/wc.jar` → chemin du jar dans le conteneur
    
- `wc.WcDriver` → classe principale avec le package `wc`
    
- `/user/root/gutenberg` → répertoire source HDFS
    
- `/user/root/wordcounts` → répertoire de sortie HDFS
    

---

### **7️⃣ Vérifier les résultats**

1. Lister le répertoire de sortie :
    

```bash
hadoop fs -ls /user/root/wordcounts
```

2. Afficher les premières lignes du résultat :
    

```bash
hadoop fs -cat /user/root/wordcounts/part-r-00000 | head -20
```

> Affiche les 20 premiers mots et leur nombre d’occurrences.

---

### **8️⃣ Récupérer le fichier sur Windows**

1. Copier depuis HDFS vers le conteneur :
    

```bash
hadoop fs -get /user/root/wordcounts/part-r-00000 /root/part-r-00000
```

2. Copier depuis le conteneur vers Windows :
    

```powershell
docker cp namenode:/root/part-r-00000 "C:\Users\adame\Desktop\TP Hadoop\Exercice 1\part-r-00000.txt"
```

✅ Maintenant le fichier est disponible sur ton Windows pour consultation.

---

## **Requêtes Hadoop utilisées**

- `hadoop fs -mkdir -p <répertoire>` → créer un répertoire HDFS
    
- `hadoop fs -put <local> <HDFS>` → copier fichier depuis conteneur vers HDFS
    
- `hadoop fs -ls <répertoire>` → lister les fichiers HDFS
    
- `hadoop fs -cat <fichier>` → afficher le contenu d’un fichier HDFS
    
- `hadoop fs -get <HDFS> <local>` → récupérer fichier HDFS dans le conteneur
    

---

## **Résumé**

- **HDFS** a été préparé et le fichier source chargé.
    
- **Projet Java** créé avec Driver, Mapper et Reducer.
    
- **Compilation Java 8** et création du jar respectant le package `wc`.
    
- **Job Hadoop MapReduce** lancé avec succès.
    
- **Résultats** vérifiés dans HDFS et récupérés sur Windows.
    

✅ Exercice 1 terminé avec succès : WordCount fonctionnel.

---

Si tu veux, je peux te faire **le même README détaillé pour tous les exercices 2, 3 et 4**, prêt à compléter ton TP 😎.

Veux‑tu que je fasse ça ?

# Exo 2
