---
tags:
  - BigData
---

# Rapport d'Analyse : Les Arbres de la Ville de Paris (Spark SQL)

Ce document détaille le procédé technique, le code utilisé et l'interprétation des résultats obtenus lors de l'analyse du jeu de données Open Data concernant le patrimoine arboré de Paris.

---

## 1. Procédé Technique

L'analyse a été réalisée en utilisant l'API **Spark SQL (DataFrames)**, car elle offre des performances supérieures pour les données structurées et permet des fonctions d'agrégation simplifiées par rapport aux RDD.

### Les étapes clés :

1. **Chargement & Inférence de schéma** : Lecture du fichier CSV avec la détection automatique des types (le système reconnaît que la hauteur est un nombre).
    
2. **Nettoyage des données** :
    
    - Suppression des lignes où le nom de l'arbre (`LIBELLE FRANCAIS`) est manquant.
        
    - Filtrage des valeurs à zéro pour la hauteur et la circonférence (mesures erronées ou arbres non encore mesurés).
        
3. **Agrégation** : Utilisation de `groupBy` pour regrouper les données par zone géographique ou par essence.
    
4. **Transformation** : Calcul des moyennes et arrondissement des résultats à deux décimales pour la lisibilité.
    

---

## 2. Le Code Source (Scala)

Scala

```
import org.apache.spark.sql.functions._

// 1. Chargement des données
val trees = spark.read.
  option("header", "true").
  option("sep", ";").
  option("inferSchema", "true").
  csv("/user/root/data/les-arbres.csv")

// 2. Exercice A : Nombre de variétés par arrondissement
val varietesArr = trees.
  filter(col("LIBELLE FRANCAIS").isNotNull).
  groupBy("ARRONDISSEMENT").
  agg(countDistinct("LIBELLE FRANCAIS").as("Nb_Varietes")).
  orderBy(desc("Nb_Varietes"))

// 3. Exercice B : Statistiques moyennes (en ignorant les zéros)
val moyennes = trees.
  filter(col("LIBELLE FRANCAIS").isNotNull).
  filter(col("CIRCONFERENCE (cm)") > 0 && col("HAUTEUR (m)") > 0).
  groupBy("LIBELLE FRANCAIS").
  agg(
    round(avg("CIRCONFERENCE (cm)"), 2).as("Circ_Moy_cm"),
    round(avg("HAUTEUR (m)"), 2).as("Haut_Moy_m")
  ).
  orderBy(desc("Haut_Moy_m"))
```

---

## 3. Résultats et Analyse

### A. Diversité par Arrondissement

Le résultat montre que le **16ème arrondissement** et le **Bois de Vincennes** sont les zones les plus diversifiées de Paris.

|**Rang**|**Arrondissement**|**Nombre de Variétés**|
|---|---|---|
|1|PARIS 16E ARRDT|156|
|2|BOIS DE VINCENNES|152|
|3|PARIS 18E ARRDT|140|
|4|PARIS 15E ARRDT|137|

**Analyse** : La présence des bois et des grands parcs historiques dans les arrondissements périphériques favorise une plus grande diversité biologique par rapport au centre de Paris (ex: le 2ème arrondissement ne compte que 42 variétés).

### B. Records de croissance par Essence

L'analyse des hauteurs moyennes nous permet d'identifier les essences les plus imposantes du patrimoine parisien.

|**Essence**|**Hauteur Moyenne (m)**|**Circonférence Moyenne (cm)**|
|---|---|---|
|**Cyprès Chauve**|16.75|175.19|
|**Sequoia**|16.63|197.54|
|**Sapin Douglas**|15.00|95.00|
|**Peuplier**|14.96|132.36|

**Analyse** :

- Le **Cyprès Chauve** et le **Sequoia** dominent le classement en hauteur, ce qui est cohérent avec la nature de ces espèces capables de croissances verticales importantes.
    
- Le **Platane** (6ème avec 13.68m) reste une essence majeure de Paris, affichant une circonférence solide de 118cm, témoignant de son implantation ancienne dans les avenues parisiennes.
    
