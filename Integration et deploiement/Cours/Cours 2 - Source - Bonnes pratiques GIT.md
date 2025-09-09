---
tags:
  - cours
  - IDC
---

## 🌱 GitFlow
![[Pasted image 20250903180236.png]]

### 🔹 main (branche principale)

- Contient uniquement du **code en production**.
    
- Chaque commit correspond à une version stable (tag v0.1, v0.2, v1.0).
    
- **Jamais de dev direct dessus** → uniquement des merges depuis `release` ou `hotfix`.
    

👉 Bonne pratique :

- Protéger la branche `main` (pas de push direct, seulement merge requests validées).
    

---

### 🔹 develop (branche de développement)

- Base de tous les développements.
    
- Code **intégré** mais pas encore prêt pour prod.
    
- Sert de "pré-prod".
    

👉 Bonne pratique :

- Toutes les `feature` branches doivent être mergées ici.
    
- Tests automatiques sur chaque merge pour garantir la stabilité.
    

---

### 🔹 feature (branches de fonctionnalités)

- Créées à partir de `develop`.
    
- Chaque feature = une branche (`feature/login`, `feature/dashboard`).
    
- Fusionnées dans `develop` quand elles sont terminées.
    

👉 Bonne pratique :

- Nommez clairement vos features (`feature/auth-api`).
    
- Supprimer la branche après merge pour éviter le désordre.
    

---

### 🔹 release (branches de livraison)

- Créées à partir de `develop` quand on prépare une version.
    
- Sert à corriger des petits bugs, stabiliser avant mise en prod.
    
- Fusionnée dans **main** (prod) et dans **develop** (pour ne pas perdre les correctifs).
    

👉 Bonne pratique :

- Exemples de nommage : `release/1.0.0`.
    
- On ne rajoute pas de nouvelles fonctionnalités ici, uniquement corrections.
    

---

### 🔹 hotfix (branches de correction d’urgence)

- Créées à partir de `main`.
    
- Utilisées pour corriger un bug critique en production.
    
- Fusionnées ensuite dans **main** (prod direct) et **develop** (pour garder la cohérence).
    

👉 Bonne pratique :

- Exemples de nommage : `hotfix/urgent-crash`, `hotfix/1.0.1`.
    
- Déploiement rapide, tests ciblés, pas de nouvelles features.
    

---

### 🚦 Workflow recommandé

1. On développe sur `feature/*` → merge dans `develop`.
    
2. Quand stable → créer une `release/x.y`.
    
3. Corriger et tester sur la release.
    
4. Déployer en prod → merge dans `main`.
    
5. Si urgence → créer `hotfix/*` depuis `main`.
    

## 🔄 Pull Requests (aussi appelées Merge Requests)

### 🎯 But

- **Relire et valider** le code avant qu’il soit intégré.
    
- Permet :
    
    - revue par les pairs (peer review),
        
    - détection de bugs ou failles,
        
    - discussions et commentaires,
        
    - déclenchement automatique des tests CI/CD.
        

### ⚡ Bonnes pratiques

- **Une PR = une fonctionnalité / un bug fix** (pas de PR “gros sac” avec 2000 lignes).
    
- **Description claire** : ce qui est fait, pourquoi, comment tester.
    
- **Assignation** : toujours demander une review à 1–2 collègues.
    
- **Tests obligatoires** : CI doit passer avant merge.
    
- **Squash & Merge** : pour garder un historique propre.
    

👉 Exemple :

- Branch `feature/login` → PR vers `develop`
    
- CI vérifie → collègues relisent → merge validé.
    

---

## 📝 Conventions de commits

### 🎯 But

- Garder un **historique clair et compréhensible**.
    
- Facilite la génération de changelogs automatiques.
    

### ✅ Format standard (Conventional Commits)
```bash
<type>(scope): <message>

```

### Types principaux

- **feat** : nouvelle fonctionnalité (`feat(auth): add login endpoint`).
    
- **fix** : correction de bug (`fix(api): prevent null crash`).
    
- **docs** : documentation (`docs(readme): update installation guide`).
    
- **style** : changements de formatage sans impact (indentation, espaces).
    
- **refactor** : refactoring sans ajout de feature.
    
- **test** : ajout/modif de tests.
    
- **chore** : tâches diverses (maj dépendances, config).
    

### ⚡ Bonnes pratiques

- **Commits petits et atomiques** (un changement précis = un commit).
    
- **Message à l’impératif** : "add login form", pas "added" ou "adding".
    
- **Toujours en anglais** (standard international).
    
- **Relire avant de commit** (éviter “fix bug”, “update stuff”).
## 🔟 Commandes Git essentielles

- **git init** → initialise un nouveau dépôt Git local.
    
- **git clone [url]** → copie un dépôt distant en local.
    
- **git status** → affiche l’état actuel des fichiers suivis et non suivis.
    
- **git add [fichier]** → ajoute un fichier ou modification à la zone de staging.
    
- **git commit -m "message"** → enregistre les changements dans l’historique avec un message.
    
- **git log** → affiche l’historique détaillé des commits.
    
- **git branch** → liste, crée ou supprime des branches.
    
- **git checkout [branche]** → change de branche ou restaure un fichier.
    
- **git merge [branche]** → fusionne une branche dans la branche courante.
    
- **git stash** → met de côté (stash) les modifications en cours pour travailler proprement.
    
- **git push / git pull** → envoie ou récupère les changements avec le dépôt distant.

