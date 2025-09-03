---
tags:
  - cours
  - IDC
---

## 🌱 GitFlow
![[Pasted image 20250903180236.png]]

## 🔹 main (branche principale)

- Contient uniquement du **code en production**.
    
- Chaque commit correspond à une version stable (tag v0.1, v0.2, v1.0).
    
- **Jamais de dev direct dessus** → uniquement des merges depuis `release` ou `hotfix`.
    

👉 Bonne pratique :

- Protéger la branche `main` (pas de push direct, seulement merge requests validées).
    

---

## 🔹 develop (branche de développement)

- Base de tous les développements.
    
- Code **intégré** mais pas encore prêt pour prod.
    
- Sert de "pré-prod".
    

👉 Bonne pratique :

- Toutes les `feature` branches doivent être mergées ici.
    
- Tests automatiques sur chaque merge pour garantir la stabilité.
    

---

## 🔹 feature (branches de fonctionnalités)

- Créées à partir de `develop`.
    
- Chaque feature = une branche (`feature/login`, `feature/dashboard`).
    
- Fusionnées dans `develop` quand elles sont terminées.
    

👉 Bonne pratique :

- Nommez clairement vos features (`feature/auth-api`).
    
- Supprimer la branche après merge pour éviter le désordre.
    

---

## 🔹 release (branches de livraison)

- Créées à partir de `develop` quand on prépare une version.
    
- Sert à corriger des petits bugs, stabiliser avant mise en prod.
    
- Fusionnée dans **main** (prod) et dans **develop** (pour ne pas perdre les correctifs).
    

👉 Bonne pratique :

- Exemples de nommage : `release/1.0.0`.
    
- On ne rajoute pas de nouvelles fonctionnalités ici, uniquement corrections.
    

---

## 🔹 hotfix (branches de correction d’urgence)

- Créées à partir de `main`.
    
- Utilisées pour corriger un bug critique en production.
    
- Fusionnées ensuite dans **main** (prod direct) et **develop** (pour garder la cohérence).
    

👉 Bonne pratique :

- Exemples de nommage : `hotfix/urgent-crash`, `hotfix/1.0.1`.
    
- Déploiement rapide, tests ciblés, pas de nouvelles features.
    

---

# 🚦 Workflow recommandé

1. On développe sur `feature/*` → merge dans `develop`.
    
2. Quand stable → créer une `release/x.y`.
    
3. Corriger et tester sur la release.
    
4. Déployer en prod → merge dans `main`.
    
5. Si urgence → créer `hotfix/*` depuis `main`.
    
