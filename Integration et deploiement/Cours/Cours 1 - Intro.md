---
tags:
  - cours
  - IDC
---
## CI/CD 

![[Pasted image 20250903175144.png]]

## 🌍 Vue d’ensemble

- CI/CD = automatisation du cycle de développement → livraison rapide et fiable.
    
- Pipeline : **Source → Verify → Package → Release → Delivery/Deployment → Prod**.
    

---

## 1) Source

> [!summary] Point de départ

- Gestion de code source (Git).
    
- Exemples : **GitHub, GitLab, Bitbucket, Azure DevOps**.



---

## 2) Verify (CI – Intégration Continue)

> [!summary] Objectif : valider la qualité du code avant la suite.

- **Analyse du code** : style, bonnes pratiques.
    
- **Build/Test** : compilation + tests unitaires/automatisés.
    
- **Vulnérabilité/Sécurité** : scan dépendances, failles containers.
    

👉 Outils courants : **SonarQube, Checkmarx, Snyk**.

---

## 3) Package

> [!summary] Objectif : produire un artefact réutilisable.

- Format : image Docker, librairie (NPM, Maven, PyPI…).
    
- Stockage : Container Registry, NPM Registry, Maven Repo.
    

👉 Exemple : une API Java packagée en `.jar`, une app front packagée en image Docker.

---

## 4) Qualité & Scan de Sécurité

- Étape de validation supplémentaire.
    
- Vérifie :
    
    - Performance,
        
    - Qualité logicielle (métriques SonarQube),
        
    - Sécurité des dépendances.
        

---

## 5) Déploiement (CD)

### 🔹 Continuous Delivery (CDv)

- Déploiement **manuel** : bouton "Deploy to Prod".
    
- Permet un contrôle humain (finance, critique).
    

### 🔹 Continuous Deployment (CDep)

- Déploiement **automatique** jusqu’en production.
    
- Nécessite une grande confiance dans la chaîne de tests.
    

👉 Environnements cibles : **Kubernetes, Terraform, Ansible**.

---

## 6) Release

- Mise à disposition des fonctionnalités validées.
    
- Techniques :
    
    - **Canary Release** (déploiement progressif),
        
    - **Feature Flags** (activer/désactiver dynamiquement).
        

---

## 7) Cloud & Infra

> [!summary] Où on déploie ?

- **Cloud Providers** : AWS, Azure, GCP, Heroku, OVH, Scaleway.
    
- **Outils d’infra** : Kubernetes (orchestration), Terraform (Infra as Code), Ansible (config auto).
    

---

## 🧰 Outils principaux résumés

- **Source** : GitHub, GitLab, Bitbucket, Azure DevOps.
    
- **Qualité/Sécu** : SonarQube, Checkmarx, Snyk, Artifactory, Nexus.
    
- **Déploiement** : Kubernetes, Terraform, Ansible.
    
- **Cloud** : AWS, Azure, GCP, OVH, Scaleway.
    
