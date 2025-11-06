---
tags:
  - exam
  - IDC
---
[[Integration et deploiement]]
## Pipeline principal du CI/CD
 Pipeline : **Source → Verify → Package → Release → Deployment → Prod**.

## Source 
Gestion de code source (exemple GitHub,GitLab)

### Branches : 
- main : Branche principale
- Release : Branche de livraison (reparation de bugs)
- develop : Branche de base de tous les ddeveloppements
- Feature : Crée à partir de Develop , permet d'ajouter des features
Merge request : Relecture test et validation du test avant de merge avec le main


### Commit conventions
Type(scope) : message
#### Types principaux
- feat : Nouvelle fonctionalité
- fix : reparation de bug
- docs : Docmentation
- refactor : refactoring sans ajout de feature

### Commandes
- git stash : mettre changements actuels de coté

## Package (Docker)

### Solution à 
problèmes de dependances, VMs chères et deploiements lourds

### Diff VM et conteneur
VM : contient un OS/ kernel complet, consomme beaucoup, lent au boot 
Conteneur : Leger , contient uniquement dependances de l'app , boot rapide

### Concepts clés 
Image : modèle en lecture seule qui contient app+deps
Conteneur : Instance d'une image
Dockerfile : script de configuration de construction d'image
Registry : depot de stocckage d'images

### Commandes principales
- docker verison : version
- docker pull : telecharger une image
- docker images : liste des images
- docker rmi : remove image
- docker build -t : construire image depuis dockerfile
- docker run : lancer un conteneur
- docker ps : liste des conteneurs actifs
- docker stop : arreter conteneur 
- docker sstart : lancer conteneur
- docker rm : supprimer conteneur
### Gitlab yaml
petit recit d'utilisation
de le yml git lab la première chose est de declarer les etapes du pipeline :
```yaml
stages:
	- build 
	- lint
	- security
	- quality
	- deploy
```
on declare defaut en suite (le prescript) : ce dernier permet de determiner la configuration par defaut 
```yaml
default:
 image: python:3.10
 before_script:
	- pip install pip
	- pip install -r requirements.txt
```
on declare ensuite les etapes du build
```yaml
build-job
	stage: build
	script:
	 - python run.py
```

on declare ensuite le lint (controle qualité)
```yaml
lint-job
 stage:lint
 script: 
  - pip install pylint
  - pylint run.py
```
on implemente ensuite la doc en utilisant sphinx
```yaml
deploy-docs
	stage: deploy
	script:
	 - pip install sphinx
	- sphinx commande
	 artifacts:
	  paths
	  - docs/build/html
	only :
	-main
```
on implente ensuite le docckerbuild
```yaml
docker-build
 stage : deploy
 image: docker:27
 services : docker:dind
 variables :
 DOCKER_HOST
 ...
```

donc la structure generale du yaml :
```yaml
stages:
- build
- lint
- security
- quality
- deploy
  
default:
	image : python:3.10
	before_script:
	- pip install -r requirements.txt

build-job:
 stage:build
 script:
	 python main.py

lint-job:
	stage:lint 
	script: 
		- pip install pylint
		-pylint main.py
deploy-doc:
	stage : deploy
	script:
		- pip install sphinx
		- commande sphinx
	artifacts:
	paths:
	doc/doc.html
	only :
	main
deploy-docker:
	stage : deploy
	
```
### Dockerfile

exemple : 
```dockerfile
# FROM : image de base
FROM python:3.11-slim  

# RUN : exécute une commande à la création de l'image
RUN pip install requests  

# COPY : copie un fichier local dans l'image
COPY app.py /app/app.py  

# CMD : commande par défaut au lancement du conteneur
CMD ["python", "/app/app.py"]

```




From : importer l'image de base 
RUN : executer une commande shell 
COPY : ajouter les fichiers necessaires dans l'image
CMD : commande par defaut pour run

### Optimisation : 
- utiliser des images plus legere comme alpine
- regrouper les RUNS en une seule commande 
- utiliser dockerignore


Astuces : 
- Pour node les images node:apline sont les plus legeres , en python c'est python:slim
- On met les fichiers de dependances en cache : package*.json
- Pour node on utilise npm ci au lieu de npm install
- on procède de façon modulaire , Builder au debut et runner après (gain de temps)
- on se base sur un utilisateur non root (securité)
###### CODE
```dockerfile
FROM python:slim AS builder

WORKDIR /app

COPY requirements.txt

RUN pip install -r requirements.txt

COPY . .


FROM python:slim AS runner

WORKDIR /app

RUN useradd -m newuser

COPY --from=builder /app/. /app

EXPOSE 3000

CMD ["python","main.py"]
```
###### CODE
```dockerfile
FROM python:slim as builder

WORKDIR /app

COPY requirements.txt


RUN pip install -r requirements.txt

COPY . .


FROM python:slim as runner

COPY --from=builder /app/. /app

RUN useradd -m newUser

USER newUser

EXPOSE 3000

CMD ["python","app.py"]



```
