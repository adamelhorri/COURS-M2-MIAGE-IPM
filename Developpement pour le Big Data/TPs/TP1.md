---
tags:
  - BigData
---
## Objectif du TP

Ce TP a pour objectif d’installer un environnement **Hadoop distribué** à l’aide de **Docker**, puis de manipuler le **Hadoop Distributed File System (HDFS)** via des commandes shell. Une vérification de l’intégration de **Apache Spark** est également réalisée.

lien : https://docs.google.com/document/d/1g1kpPRdvlmZhkRCRQ0br3ODz2uI9A4kWnvSy0vpq5x8/edit?tab=t.0

---

## 1. Installation de l’environnement

### 1.1 Installation de WSL (Windows Subsystem for Linux)

Commande exécutée sous PowerShell :

```
wsl --install
```

**Explication :**  
WSL permet d’exécuter un environnement Linux sous Windows, indispensable pour une bonne compatibilité avec Docker.

---

### 1.2 Installation de Docker Desktop

Docker Desktop a été installé depuis le site officiel et lancé avec les options par défaut.

**Rôle de Docker :**  
Docker permet de lancer Hadoop sous forme de conteneurs, évitant une installation complexe locale.

---

## 2. Lancement du cluster Hadoop

### 2.1 Récupération du projet Docker-Hadoop

Le projet est basé sur le dépôt :

> [https://github.com/big-data-europe/docker-hadoop](https://github.com/big-data-europe/docker-hadoop)

Le dossier a été téléchargé et décompressé.

---

### 2.2 Démarrage des conteneurs Hadoop

Commande exécutée dans le dossier Docker-Hadoop :

```
docker-compose up -d
```

**Explication :**  
Cette commande lance les conteneurs Hadoop (namenode, datanode, resourcemanager…) en arrière-plan.

Arrêt possible avec :

```
docker-compose down
```

---

## 3. Accès au Namenode et vérification de Hadoop

### 3.1 Accès au conteneur namenode

```
docker exec -it namenode bash
```

**Explication :**  
Permet d’ouvrir un terminal bash directement dans le conteneur maître Hadoop (namenode).

---

### 3.2 Vérification de l’installation de Hadoop

```
hadoop version
```

**Résultat attendu :**  
Affichage de la version de Hadoop confirmant son bon fonctionnement.

---

## 4. Installation et test de Spark

### 4.1 Copie de Spark vers le namenode

Commande exécutée depuis PowerShell :

```
docker cp spark-3.1.2-bin-hadoop3.2 namenode:/opt/spark-3.1.2
```

**Explication :**  
Apache Spark est copié dans le conteneur Hadoop afin de fonctionner avec HDFS.

---

### 4.2 Test de Spark

```
/opt/spark-3.1.2/bin/spark-shell
```

**Résultat attendu :**  
Affichage de la version de Spark et accès à l’invite `scala>`.

---

## 5. Manipulation du Hadoop File System (HDFS)

### 5.1 Création du répertoire utilisateur root

```
hadoop fs -mkdir -p /user/root
```

**Explication :**  
Chaque utilisateur Hadoop possède un répertoire personnel dans HDFS.

---

### 5.2 Copie du fichier weblog_entries.txt vers le namenode

```
docker cp weblog_entries.txt namenode:/root/
```

**Explication :**  
Le fichier est d’abord copié de la machine locale vers le conteneur Docker.

---

### 5.3 Création de l’arborescence HDFS

```
hadoop fs -mkdir -p /user/root/data/weblogs
```

---

### 5.4 Copie du fichier vers HDFS

```
hadoop fs -put /root/weblog_entries.txt /user/root/data/weblogs/
```

**Explication :**  
Le fichier est transféré du système local du conteneur vers HDFS.

---

### 5.5 Vérification du contenu

```
hadoop fs -ls /user/root/data/weblogs
```

---

### 5.6 Copie et renommage du fichier dans HDFS

```
hadoop fs -mkdir -p /user/root/data/web
hadoop fs -cp /user/root/data/weblogs/weblog_entries.txt /user/root/data/web/log.txt
```

**Explication :**  
Cette opération duplique un fichier à l’intérieur de HDFS avec un nouveau nom.

---

### 5.7 Affichage des dernières lignes du fichier

```
hadoop fs -tail /user/root/data/web/log.txt
```

**Explication :**  
Permet de visualiser les dernières lignes d’un fichier stocké dans HDFS.

---

### 5.8 Suppression du répertoire weblogs

```
hadoop fs -rm -r /user/root/data/weblogs
```

**Explication :**  
Suppression récursive d’un répertoire HDFS.

---

### 5.9 Récupération du fichier depuis HDFS vers le bash

```
hadoop fs -get /user/root/data/web/log.txt /root/
```

**Explication :**  
Permet de rapatrier un fichier HDFS vers le système local du conteneur.

---

## 6. Interface Web Hadoop

Accès via navigateur :

```
http://localhost:9870
```

**Fonctionnalités utilisées :**

- Utilities
    
- Browse the file system
    

Cette interface permet de visualiser graphiquement les fichiers HDFS.

---

## Conclusion

Ce TP a permis :

- L’installation complète de Hadoop sous Docker
    
- La compréhension de l’architecture HDFS
    
- La manipulation des fichiers distribués via le shell Hadoop
    
- L’intégration et la validation de Spark
    

L’environnement est désormais prêt pour des traitements Big Data distribués.