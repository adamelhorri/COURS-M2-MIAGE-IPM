---
tags:
  - cours
  - IDC
---
## 🔹Problématiques & Solutions

- **Avant Docker** :
    
    - “Ça marche sur ma machine” → dépendances différentes entre dev, test, prod.
        
    - Déploiements lourds, longs, non reproductibles.
        
    - VMs consomment beaucoup de ressources (OS complet à chaque fois).
        
- **Avec Docker** :
    
    - Isolation légère → chaque app a son environnement propre.
        
    - Portabilité → même conteneur tourne partout (dev, cloud, prod).
        
    - Rapidité → lancement en secondes, scaling facile.
        
    - Standardisation → pipelines CI/CD simplifiés.
        

---

## 🔹 Différences VM vs Conteneurs

- **VM (Virtual Machine)** :
    
    - Inclut un OS complet (Kernel + app).
        
    - Plus lourd → consomme CPU/RAM/disque.
        
    - Boot lent (minutes).
        
- **Conteneur (Docker)** :
    
    - Partage le kernel de l’hôte, contient uniquement app + dépendances.
        
    - Très léger → moins de ressources.
        
    - Boot rapide (secondes).
        
    - Idéal pour microservices et CI/CD.
        

---

## 🔹 Concepts Clés Docker

- **Image** : modèle en lecture seule (template) qui contient l’app + dépendances.
    
    - Exemple : `python:3.10` est une image officielle Python.
        
- **Conteneur** : instance en cours d’exécution d’une image.
    
    - Exemple : un conteneur basé sur `mysql:8` qui tourne comme base de données.
        
- **Dockerfile** : script de configuration qui décrit comment construire une image.
    
    - Exemple : définir l’OS de base, copier le code, installer dépendances, lancer service.
        
- **Registry** : dépôt centralisé pour stocker/partager les images.
    
    - Exemple : Docker Hub (public), GitLab Container Registry (privé).
## 🔹 L’architecture de Docker

- **Client** : interface en ligne de commande (`docker run`, `docker build`…), envoie les instructions.
    
- **API REST** : intermédiaire qui traduit les commandes du client vers le moteur.
    
- **Docker Engine (daemon)** : cœur de Docker → crée, exécute et gère les conteneurs.
    

---

## 🔹 Cas d’utilisation de Docker

- **Dev local** : simuler un environnement identique à la prod.
    
- **CI/CD** : exécuter tests, builds et déploiements reproductibles.
    
- **Multi-environnements** : même image pour dev, test, prod.
    
- **Microservices** : chaque service dans son conteneur.
    
- **Déploiement** : scaling rapide dans le cloud (Kubernetes, Swarm).
    

---

## 🔹 Commandes principales Docker (top 20)

- **docker version** → afficher la version installée.
    
- **docker info** → infos système et config Docker.
    
- **docker pull [image]** → télécharger une image.
    
- **docker images** → lister les images disponibles.
    
- **docker rmi [image]** → supprimer une image.
    
- **docker build -t [nom] .** → construire une image depuis un Dockerfile.
    
- **docker run [image]** → lancer un conteneur.
    
- **docker ps** → lister les conteneurs en cours d’exécution.
    
- **docker ps -a** → lister tous les conteneurs (même stoppés).
    
- **docker stop [id]** → arrêter un conteneur.
    
- **docker start [id]** → relancer un conteneur.
    
- **docker restart [id]** → redémarrer un conteneur.
    
- **docker rm [id]** → supprimer un conteneur.
    
- **docker exec -it [id] bash** → entrer dans un conteneur en cours.
    
- **docker logs [id]** → afficher les logs d’un conteneur.
    
- **docker network ls** → lister les réseaux Docker.
    
- **docker volume ls** → lister les volumes.
    
- **docker-compose up -d** → démarrer une app multi-conteneurs.
    
- **docker-compose down** → arrêter et supprimer les conteneurs d’un projet.
    
- **docker system prune** → nettoyer images/volumes/conteneurs inutilisés.

## 🔹 Les volumes et ports

- **Volumes** : stockage persistant pour les données (ex : BDD).
    
    - Exemple : `docker run -v /data:/var/lib/mysql mysql:8`
        
- **Ports** : exposition d’un service interne vers l’extérieur.
    
    - Exemple : `docker run -p 8080:80 nginx` (mappe port local 8080 → port 80 du conteneur).
        

---

## 🔹 Les layers dans un Dockerfile

- **FROM** : image de base.
    
- **RUN** : exécute une commande lors de la création de l’image.
    
- **COPY / ADD** : copie des fichiers dans l’image.
    
- **CMD / ENTRYPOINT** : définit la commande par défaut au lancement du conteneur.
    

---

## 🔹 Optimiser les layers

- **Choix** : utiliser une image de base légère (`alpine` au lieu de `ubuntu`).
    
- **Fusion** : regrouper plusieurs `RUN` en une seule commande pour limiter les couches.
    
- **.dockerignore** : exclure fichiers inutiles (logs, node_modules).
    
- **Multi-stage builds** : compiler dans une image lourde → copier uniquement le résultat dans une image légère.
    

👉 Exemple :
```dockerfile
# Étape 1 : build
FROM node:20 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Étape 2 : prod
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

```


