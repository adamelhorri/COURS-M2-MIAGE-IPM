---
tags:
  - back
  - exos
---

# **1. Architectures & Web Basics**

## 1.1 Architectures

### ❓ Q1 — Qu’est-ce qu’une architecture 1-tier ?
- [ ] Tout est réparti sur plusieurs serveurs
- [ ] Client + logique métier + BD séparés
- [ ] Plusieurs couches indépendantes
- [ ] Tout est sur un seul serveur

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Rien n’est distribué.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  Tout est sur **un seul serveur** (UI + logique + données).
</details>

---

### ❓ Q2 — Avantage principal du 1-tier
- [ ] Très scalable
- [ ] Très simple
- [ ] Client léger
- [ ] Très sécurisé

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Facile à mettre en place.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  **Simplicité** et centralisation.
</details>

---

### ❓ Q3 — Dans le 2-tiers, que contient le client ?
- [ ] Un simple navigateur
- [ ] Interface + logique métier
- [ ] BD + tables
- [ ] Serveur applicatif

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Il interroge directement la BD.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  Le client contient **UI + logique**, et interroge directement le SGBD.
</details>

---

### ❓ Q4 — Limite majeure du 2-tiers
- [ ] Client léger
- [ ] Couplage fort au SGBD
- [ ] Trop de serveurs à gérer
- [ ] Pas de logique métier

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  La BD dépend directement de l’application cliente.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  **Couplage fort** : le client dépend trop du SGBD.
</details>

---

### ❓ Q5 — Les 3 tiers du modèle 3-tiers
- [ ] Client
- [ ] Serveur d’applications
- [ ] Serveur BD
- [ ] Proxy réseau

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  C’est le classique Client / Métier / Données.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  **Client**, **Serveur d’applications**, **Serveur BD**.
</details>

---

### ❓ Q6 — Avantage principal du 3-tiers
- [ ] Très peu de serveurs
- [ ] Séparation claire des responsabilités
- [ ] Client lourd obligatoire
- [ ] Pas de logique métier

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Permet l’évolution et la répartition de charge.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  **Séparation claire**, meilleure évolutivité et scalabilité.
</details>

---

### ❓ Q7 — Caractéristique d’une architecture n-tiers
- [ ] Tout tourne sur un PC unique
- [ ] Multiplication des serveurs spécialisés
- [ ] Aucun serveur applicatif
- [ ] Architecture ultra-simple

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Plusieurs services répartis.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  **Multiples serveurs spécialisés** (web, API, métier, BD…).
</details>

---

### ❓ Q8 — Quel type de client est installé localement ?
- [ ] Client léger
- [ ] Client lourd
- [ ] Client riche
- [ ] Aucun

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Dépend du système d’exploitation.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  Le **client lourd**.
</details>

---

### ❓ Q9 — Quel type de client fonctionne uniquement dans un navigateur ?
- [ ] Client lourd
- [ ] Client léger
- [ ] Client riche
- [ ] Client embarqué

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Nécessite zéro installation.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  Le **client léger**.
</details>

---

### ❓ Q10 — Le client riche correspond à :
- [ ] Un navigateur sans JS
- [ ] Un web client avec interactions avancées
- [ ] Une application installée
- [ ] Un micro-service

<details>
  <summary>➡️ Voir l'indice</summary>

  **Indice :**  
  Web + dynamique avancée.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>

  **Réponse :**  
  Un **client web très interactif** (JS, AJAX…).
</details>


## 1.2/ 1.3 Standards Web / Pages dynamiques

### ❓ Q1 — Quel est le rôle principal du langage HTML ?
- [ ] Gérer la logique métier
- [ ] Structurer le contenu d’une page Web
- [ ] Gérer les connexions réseau
- [ ] Exécuter du code serveur

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Balises, titres, paragraphes.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Structurer la page Web.**
</details>

---

### ❓ Q2 — Quels sont les verbes HTTP de base utilisés dans les applications Web ?
- [ ] RUN / STOP / PUSH / PULL
- [ ] GET / POST / PUT / DELETE
- [ ] FETCH / SEND / DELETE / SYNC
- [ ] LOAD / WRITE / EXECUTE / REMOVE

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  REST utilise ce quatuor.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **GET, POST, PUT, DELETE.**
</details>

---

### ❓ Q3 — Que transporte TCP/IP ?
- [ ] Les images d’un site Web
- [ ] Des scripts JavaScript
- [ ] Les paquets réseau (transport + adressage)
- [ ] Le code CSS uniquement

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  C’est la base fondamentale d’Internet.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Des paquets réseau (transport + réseau).**
</details>

---

### ❓ Q4 — Que faisait CGI ?
- [ ] Servait à styliser les pages Web
- [ ] Exécutait des programmes serveur pour générer du HTML
- [ ] Transformait le CSS en XML
- [ ] Transférait les scripts JS au navigateur

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Ancêtre des servlets et PHP.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Exécutait des scripts serveur générant du HTML.**
</details>

---

### ❓ Q5 — Quel est l’inconvénient majeur du CGI ?
- [ ] Pas compatible HTML5
- [ ] Un nouveau processus lancé pour chaque requête
- [ ] Nécessite Java
- [ ] Ne supporte pas les formulaires

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Très lourd et lent.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Un processus est créé à chaque requête → surcharge.**
</details>

---

### ❓ Q6 — Quel rôle joue JavaScript côté client ?
- [ ] Gérer les accès BD
- [ ] Valider, interagir, faire de l’AJAX
- [ ] Interpréter les servlets
- [ ] Compiler le HTML

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Il tourne dans le navigateur.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Interactions, **validation**, **AJAX**.
</details>

---

### ❓ Q7 — Dans une page dynamique côté serveur, qui génère le HTML ?
- [ ] Le navigateur
- [ ] Le programme serveur (Servlet/JSP/PHP)
- [ ] TCP/IP
- [ ] JavaScript

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  C’est exécuté avant d’envoyer la réponse au client.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Le **programme serveur**.
</details>

---

### ❓ Q8 — Dans le cycle HTTP, à quel moment intervient JavaScript ?
- [ ] Après la requête serveur
- [ ] Avant même l’envoi (contrôles formulaire)
- [ ] Pendant l’analyse SQL
- [ ] Pendant la création de session

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Le navigateur peut refuser d’envoyer une requête mal remplie.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Avant l’envoi**, pour vérifier formulaire ou interagir.
</details>

---

### ❓ Q9 — Quel verbe HTTP rend visibles les paramètres dans l’URL ?
- [ ] DELETE
- [ ] POST
- [ ] PUT
- [ ] GET

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  ?param=valeur
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **GET.**
</details>

---

### ❓ Q10 — Quel verbe HTTP permet d’envoyer des données « cachées » ?
- [ ] GET
- [ ] POST
- [ ] DELETE
- [ ] TRACE

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Utilisé pour les formulaires.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **POST.**
</details>

---

### ❓ Q11 — Quel composant interprète une requête HTTP sur le serveur ?
- [ ] Le navigateur
- [ ] Le serveur Web
- [ ] Le fichier CSS
- [ ] Le moteur TCP/IP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  C’est Apache/Tomcat/Nginx.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Le serveur Web.**
</details>

---

### ❓ Q12 — Qu’est-ce qui déclenche l’interprétation serveur d’un fichier ?
- [ ] La taille du fichier
- [ ] Son extension (.jsp, .php, .cgi)
- [ ] Presence de CSS
- [ ] Le protocole IP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Tomcat → .jsp  
  PHP → .php
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Son **extension**.
</details>

---

### ❓ Q13 — Dans la chaîne Client → Serveur → BD → Serveur → Client, qui exécute SQL ?
- [ ] Le client
- [ ] Le serveur BD
- [ ] JavaScript
- [ ] HTML

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  MySQL, PostgreSQL…
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  La **BD** (SGBD).
</details>

---

### ❓ Q14 — À quoi sert AJAX ?
- [ ] Recharger la page entièrement
- [ ] Faire des requêtes HTTP en arrière-plan
- [ ] Compiler HTML
- [ ] Exécuter SQL dans JS

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Permet d’actualiser une partie de page.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Envoyer des requêtes **asynchrones** sans recharger.
</details>

---

### ❓ Q15 — Dans GET, où sont placés les paramètres ?
- [ ] Dans le corps de la requête
- [ ] Dans les cookies
- [ ] Dans l’URL après '?'
- [ ] Dans le header Authorization

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  /page?x=1&y=2
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Dans l’**URL**.
</details>

---

### ❓ Q16 — Dans POST, où sont placés les paramètres ?
- [ ] Dans l’URL
- [ ] Dans le corps de la requête
- [ ] Dans un fichier temporaire
- [ ] Compilés en Java

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Invisible dans la barre d’adresse.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Dans le **corps** de la requête.
</details>

---

### ❓ Q17 — Qui décide quel moteur exécuter (JSP, PHP, CGI…) ?
- [ ] Le navigateur
- [ ] L’utilisateur
- [ ] Le serveur Web
- [ ] Le SGBD

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  En fonction du fichier reçu.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Le **serveur Web**.
</details>

---

### ❓ Q18 — Quel est l’ordre des étapes HTTP d’un formulaire ?
- [ ] BD → Serveur → Client → JS
- [ ] JS → Client → Serveur
- [ ] Saisie → JS → Requête → Programme → BD → HTML
- [ ] Saisie → BD → JS → HTML

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Voir le diagramme du cours.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Saisie → JS → Requête → Programme → BD → HTML.**
</details>

---

### ❓ Q19 — Quel est le rôle d’un programme serveur dans une page dynamique ?
- [ ] Lire le CSS
- [ ] Générer du HTML dynamique
- [ ] Exécuter JavaScript
- [ ] Charger TCP/IP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Fournit la page finale envoyée au client.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Générer du HTML dynamique**.
</details>

---

### ❓ Q20 — Que représente l’URL `protocole://hôte:port/ressource?param=val` ?
- [ ] Une requête SQL
- [ ] Une structure JSON
- [ ] Une requête HTTP GET
- [ ] Un paquet TCP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Contient des paramètres visibles.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Une **requête GET**.
</details>


---

# **2.3. Servlets** / JSP

### ❓ Q1 — Quel est le rôle principal d’une servlet ?
- [ ] Exécuter du JavaScript côté client
- [ ] Générer du HTML dynamique côté serveur
- [ ] Styliser les pages HTML
- [ ] Compiler les pages JSP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Comparable à une « page Java côté serveur ».
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Générer du **HTML dynamique** côté serveur.
</details>

---

### ❓ Q2 — Pourquoi dit-on qu’une servlet est rapide ?
- [ ] Elle s’exécute sur le GPU
- [ ] Elle est instanciée une seule fois et reste en mémoire
- [ ] Elle ne passe jamais par la JVM
- [ ] Elle ne gère pas les requêtes HTTP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Pas de recréation à chaque requête.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Une servlet **reste en mémoire** et ne se réinstancie pas.
</details>

---

### ❓ Q3 — Pourquoi une servlet est portable ?
- [ ] Écrite en C
- [ ] Écrite en Java
- [ ] Écrite en HTML
- [ ] Écrite en JavaScript

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  JVM.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Parce qu’elle est écrite en **Java**.
</details>

---

### ❓ Q4 — Quel mécanisme permet à une servlet de gérer plusieurs requêtes simultanément ?
- [ ] Multiprocessing
- [ ] Multithreading
- [ ] Multi-VM
- [ ] Multi-HTTP

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Plusieurs threads appellent service().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Multithreading**.
</details>

---

### ❓ Q5 — Le cycle de vie d’une servlet commence par :
- [ ] doGet
- [ ] destroy
- [ ] init
- [ ] chargement de la classe

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Avant init().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Chargement** de la classe par le moteur servlet.
</details>

---

### ❓ Q6 — Quelle méthode est appelée à chaque requête ?
- [ ] init()
- [ ] destroy()
- [ ] doGet() ou doPost() via service()
- [ ] main()

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Deux méthodes selon GET/POST.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **service() → doGet/doPost**.
</details>

---

### ❓ Q7 — La méthode init() sert à :
- [ ] Libérer les ressources
- [ ] Initialiser l’instance
- [ ] Renvoyer du HTML
- [ ] Supprimer la session

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Appelée une fois au démarrage.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Initialisation** de la servlet.
</details>

---

### ❓ Q8 — Quel objet contient les paramètres d’un formulaire ?
- [ ] HttpServletResponse
- [ ] HttpServletRequest
- [ ] ServletOutputStream
- [ ] JSPWriter

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  getParameter().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **HttpServletRequest**.
</details>

---

### ❓ Q9 — Quel objet permet de renvoyer du HTML ?
- [ ] HttpServletRequest
- [ ] HttpServletResponse
- [ ] HttpServletSession
- [ ] HttpServer

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  getWriter().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **HttpServletResponse**.
</details>

---

### ❓ Q10 — Comment récupérer un paramètre « nom » ?
- [ ] request.read("nom")
- [ ] request.get("nom")
- [ ] request.getParameter("nom")
- [ ] request.value("nom")

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Méthode classique GET/POST.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `request.getParameter("nom")`
</details>

---

### ❓ Q11 — Quel type MIME indique qu’on renvoie du HTML ?
- [ ] text/plain
- [ ] text/html
- [ ] application/json
- [ ] application/xml

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Toujours utilisé en servlet.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **text/html**
</details>

---

### ❓ Q12 — Qu’est-ce qu’une JSP ?
- [ ] Un script Python
- [ ] Une page HTML enrichie avec Java intégré
- [ ] Une servlet compilée à la main
- [ ] Un fichier CSS dynamique

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  HTML dominant.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Page **HTML + Java intégré**.
</details>

---

### ❓ Q13 — Que devient une JSP lors de son exécution ?
- [ ] Un fichier XML
- [ ] Une servlet Java
- [ ] Un fichier CSS
- [ ] Un contrôleur Spring

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Le moteur JSP génère un .java.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Une **servlet compilée**.
</details>

---

### ❓ Q14 — Que fait une directive JSP `<%@ page ... %>` ?
- [ ] Insère du HTML
- [ ] Import ou configuration de la page
- [ ] Exécute du code Java
- [ ] Crée une classe Java

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  import, errorPage…
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Configure la **page JSP**.
</details>

---
### ❓ Q15 — Quelle balise JSP insère une expression Java ?
- [ ] ◀️% %▶️
- [ ] ◀️%! %▶️
- [ ] ◀️%= %▶️
- [ ] ◀️jsp:useBean▶️

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Affiche directement la valeur d'une expression.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  ◀️%= %▶️
</details>

---

### ❓ Q16 — Quelle balise JSP permet d’inclure un fichier lors de la compilation ?
- [ ] ◀️% %▶️
- [ ] ◀️jsp:forward▶️
- [ ] ◀️%@ include %▶️
- [ ] ◀️jsp:param▶️

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Inclusion statique.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  ◀️%@ include %▶️
</details>

---

### ❓ Q17 — Quel objet implicite JSP écrit dans la réponse ?
- [ ] session
- [ ] application
- [ ] out
- [ ] request

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Équivalent de response.getWriter().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **out**
</details>

---

### ❓ Q18 — Quel objet implicite donne accès à la session ?
- [ ] out
- [ ] config
- [ ] session
- [ ] servlet

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Utilisé pour stocker panier, login, variables.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **session**
</details>

---

### ❓ Q19 — À quoi sert ◀️jsp:useBean▶️ ?
- [ ] Importer une page HTML
- [ ] Instancier ou récupérer un JavaBean
- [ ] Exécuter du JavaScript
- [ ] Lire un cookie

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Utilisé dans MVC pour le modèle.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Instancier ou récupérer un JavaBean.**
</details>

---

### ❓ Q20 — Quel tag JSP permet de rediriger ?
- [ ] ◀️jsp:include▶️
- [ ] ◀️jsp:forward▶️
- [ ] ◀️jsp:setProperty▶️
- [ ] ◀️%= %▶️

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Redirection interne côté serveur.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  ◀️jsp:forward▶️
</details>

---

### ❓ Q21 — Que fait ◀️jsp:getProperty▶️ ?
- [ ] Modifie une propriété
- [ ] Récupère une propriété du bean et l'affiche
- [ ] Exécute une requête SQL
- [ ] Écrit un cookie

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Complément de jsp:useBean.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Affiche une propriété du JavaBean.**
</details>

---

### ❓ Q22 — Quel composant transforme une JSP en servlet ?
- [ ] JVM
- [ ] Serveur BD
- [ ] Moteur JSP
- [ ] Navigateur

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Produit le fichier JSP.java.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Le **moteur JSP**.
</details>

---

### ❓ Q23 — La méthode destroy() est appelée :
- [ ] À chaque requête
- [ ] À la première requête
- [ ] À l’arrêt du moteur servlet
- [ ] Lors d’un forward

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Opposée de init().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **À l’arrêt du moteur servlet.**
</details>

---

### ❓ Q24 — Quelle méthode permet de définir le type de contenu ?
- [ ] request.setType()
- [ ] response.setMime()
- [ ] response.setContentType()
- [ ] request.setContent()

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Méthode courante en doGet().
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `response.setContentType()`
</details>

---

### ❓ Q25 — Que fait response.sendRedirect() ?
- [ ] Redirection serveur
- [ ] Redirection côté client
- [ ] Inclusion JSP
- [ ] Modification de session

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  L’URL change réellement.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Redirection **client**.
</details>

---

### ❓ Q26 — Comment lit-on un paramètre dans doPost() ?
- [ ] request.input()
- [ ] request.value()
- [ ] request.getParameter()
- [ ] request.getData()

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Identique à GET.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `request.getParameter()`
</details>

---

### ❓ Q27 — Différence entre doGet et doPost ?
- [ ] Aucune
- [ ] GET place les données dans l’URL, POST dans le corps
- [ ] POST supprime les cookies
- [ ] GET crée une nouvelle session

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Visible vs non visible.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  GET → URL  
  POST → Corps de requête
</details>

---

### ❓ Q28 — Quel tag JSP inclut dynamiquement du contenu ?
- [ ] ◀️%@ include %▶️
- [ ] ◀️jsp:include▶️
- [ ] ◀️jsp:param▶️
- [ ] ◀️%= %▶️

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Exécuté au runtime.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  ◀️jsp:include▶️
</details>

---

### ❓ Q29 — Que fait `${param.nom}` en JSP ?
- [ ] Exécute du Java
- [ ] Retourne un paramètre HTTP
- [ ] Exécute une requête BD
- [ ] Modifie une session

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Expression Language.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Retourne un paramètre HTTP** nommé “nom”.
</details>

---

### ❓ Q30 — Le schéma global Servlets + JSP représente :
- [ ] Une BD relationnelle
- [ ] La structure interne du navigateur
- [ ] Le flux Client → Servlets/JSP → HTML → Client
- [ ] Un programme JavaFX

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Voir le dernier schéma du cours.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  Le flux complet **Client ↔ Servlets/JSP ↔ HTML**.
</details>
---

### ❓ Q31 — Dans une servlet, comment effectuer un forward vers une JSP ?
- [ ] response.forward("page.jsp")
- [ ] request.getDispatcher("page.jsp").send()
- [ ] request.getRequestDispatcher("page.jsp").forward(request, response)
- [ ] request.forward("page.jsp")

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Le forward appartient au RequestDispatcher.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `request.getRequestDispatcher("page.jsp").forward(request, response)`
</details>

---

### ❓ Q32 — Lors d’un forward, où place-t-on les données pour les envoyer à la JSP ?
- [ ] Dans les cookies
- [ ] Dans les URL parameters
- [ ] Dans request.setAttribute()
- [ ] Dans des variables globales

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Portée limitée à la requête.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `request.setAttribute()`
</details>

---

### ❓ Q33 — Comment récupérer un attribut envoyé via forward dans la JSP ?
- [ ] ${attr}
- [ ] ${requestScope.attr}
- [ ] ${session.attr}
- [ ] ${header.attr}

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Expression Language (EL).
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `${requestScope.attr}`
</details>

---

### ❓ Q34 — Quelle différence entre forward et sendRedirect ?
- [ ] forward = client ; redirect = serveur
- [ ] forward = serveur ; redirect = client
- [ ] les deux sont identiques
- [ ] redirect ne change jamais l’URL

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Avec redirect, l’URL dans la barre change.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **forward = serveur** / **redirect = client**
</details>

---

### ❓ Q35 — Lors d’un POST, où se trouvent les données envoyées au serveur ?
- [ ] Dans la session
- [ ] Dans l’URL
- [ ] Dans le corps de la requête
- [ ] Dans un cookie temporaire

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Invisible dans la barre d’adresse.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Dans le corps de la requête.**
</details>

---

### ❓ Q36 — Quel objet crée-t-on pour écrire directement dans la réponse HTML ?
- [ ] request.getWriter()
- [ ] response.getWriter()
- [ ] response.getOutput()
- [ ] session.getWriter()

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  On écrit dans la réponse.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `response.getWriter()`
</details>

---

### ❓ Q37 — Dans un formulaire HTML, comment une JSP lit-elle un champ « login » envoyé ?
- [ ] ${response.login}
- [ ] ${param.login}
- [ ] ${post.login}
- [ ] ${field.login}

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Le scope param correspond aux GET/POST.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `${param.login}`
</details>

---

### ❓ Q38 — Dans une servlet, comment récupère-t-on la session utilisateur ?
- [ ] request.openSession()
- [ ] session.get()
- [ ] request.getSession()
- [ ] response.getSession()

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Contient panier, login, etc.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `request.getSession()`
</details>

---

### ❓ Q39 — Dans une JSP, comment accède-t-on à une variable de session nommée « user » ?
- [ ] ${sessionScope.user}
- [ ] ${param.user}
- [ ] ${request.user}
- [ ] ${cookie.user}

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Cookie ≠ session.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `${sessionScope.user}`
</details>

---

### ❓ Q40 — Quelle méthode Servlet gère par défaut les requêtes GET ?
- [ ] doPost
- [ ] init
- [ ] doGet
- [ ] destroy

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Utilisée quand on clique sur un lien ou tape une URL.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `doGet`
</details>

---

### ❓ Q41 — Comment spécifier le type de réponse JSON dans une servlet ?
- [ ] response.mime("json")
- [ ] response.setHeader("json")
- [ ] response.setJSON()
- [ ] response.setContentType("application/json")

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Même méthode qu’avec HTML.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  `response.setContentType("application/json")`
</details>

---

### ❓ Q42 — Quel mécanisme permet de filtrer, modifier ou bloquer une requête avant la servlet ?
- [ ] Les beans
- [ ] Les filtres (Filter)
- [ ] Les directives JSP
- [ ] Les sessions

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Chaînage très utile en sécurité.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Les filtres Servlet (Filter).**
</details>

---

### ❓ Q43 — Une JSP peut appeler une servlet via :
- [ ] Une inclusion JSP
- [ ] Une redirection ou un formulaire
- [ ] Une variable Java locale
- [ ] Le tag ◀️jsp:java▶️

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Méthode du TP pour envoyer les données.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Formulaire ou redirection vers la servlet.**
</details>

---

### ❓ Q44 — Dans une JSP, le tag ◀️%= %▶️ sert à :
- [ ] Déclarer une méthode
- [ ] Exécuter du Java sans l’afficher
- [ ] Insérer la valeur d’une expression Java
- [ ] Importer un fichier

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  C’est l’équivalent de println.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **Afficher une expression Java.**
</details>

---

### ❓ Q45 — Quel est l'ordre correct d’un cycle servlet ?
- [ ] init → destroy → service
- [ ] service → init → destroy
- [ ] destroy → init → service
- [ ] init → service → destroy

<details>
  <summary>➡️ Voir l'indice</summary>
  **Indice :**  
  Comme un cycle de vie classique.
</details>

<details>
  <summary>➡️ Voir la réponse</summary>
  **Réponse :**  
  **init → service → destroy**
</details>


---

# **4. MVC (Web Java)**
### ❓ Q1 — Quel est l’objectif principal du modèle MVC ?
- [ ] Charger la BD à chaque requête
- [ ] Séparer métier, présentation et interaction utilisateur
- [ ] Styliser les pages Java
- [ ] Remplacer les Servlets

<details><summary>➡️ Voir l'indice</summary>
Raison de la maintenance facile.
</details>

<details><summary>➡️ Voir la réponse</summary>
Séparer **métier / présentation / interaction utilisateur**.
</details>

---

### ❓ Q2 — Quel élément gère la logique métier dans MVC ?
- [ ] Vue
- [ ] Contrôleur
- [ ] Modèle
- [ ] JSP

<details><summary>➡️ Voir l'indice</summary>
JavaBeans.
</details>

<details><summary>➡️ Voir la réponse</summary>
Le **Modèle**.
</details>

---

### ❓ Q3 — Quel composant gère l’affichage dans MVC ?
- [ ] Servlet
- [ ] JavaBean
- [ ] JSP
- [ ] BD

<details><summary>➡️ Voir l'indice</summary>
HTML dominant + EL.
</details>

<details><summary>➡️ Voir la réponse</summary>
La **JSP** (Vue).
</details>

---

### ❓ Q4 — Quel composant reçoit et interprète les actions utilisateur ?
- [ ] Vue
- [ ] Contrôleur
- [ ] Modèle
- [ ] SGBD

<details><summary>➡️ Voir l'indice</summary>
Toujours une servlet.
</details>

<details><summary>➡️ Voir la réponse</summary>
Le **Contrôleur**.
</details>

---

### ❓ Q5 — Dans MVC Web Java, le contrôleur est :
- [ ] Une JSP
- [ ] Une servlet
- [ ] Un fichier XML
- [ ] Un fichier CSS

<details><summary>➡️ Voir l'indice</summary>
Reçoit requêtes HTTP.
</details>

<details><summary>➡️ Voir la réponse</summary>
Une **Servlet**.
</details>

---

### ❓ Q6 — Dans MVC Web Java, le modèle est :
- [ ] La JSP
- [ ] Le JavaBean
- [ ] Le fichier HTML
- [ ] Le listener

<details><summary>➡️ Voir l'indice</summary>
Contient les données.
</details>

<details><summary>➡️ Voir la réponse</summary>
Le **JavaBean**.
</details>

---

### ❓ Q7 — Quel composant MVC met en forme l’état du modèle ?
- [ ] Modèle
- [ ] Contrôleur
- [ ] Vue
- [ ] BD

<details><summary>➡️ Voir l'indice</summary>
Affiche.
</details>

<details><summary>➡️ Voir la réponse</summary>
La **Vue**.
</details>

---

### ❓ Q8 — Une JSP doit être utilisée pour :
- [ ] La logique métier
- [ ] Le routage HTTP
- [ ] L’affichage
- [ ] La gestion de session

<details><summary>➡️ Voir l'indice</summary>
HTML dominant.
</details>

<details><summary>➡️ Voir la réponse</summary>
L’**affichage**.
</details>

---

### ❓ Q9 — Le contrôleur appelle la vue via :
- [ ] response.sendHTML()
- [ ] request.forward()
- [ ] request.sendData()
- [ ] session.show()

<details><summary>➡️ Voir l'indice</summary>
Méthode du TP.
</details>

<details><summary>➡️ Voir la réponse</summary>
**forward()** via RequestDispatcher.
</details>

---

### ❓ Q10 — Quel composant met à jour le modèle ?
- [ ] JSP
- [ ] Servlet
- [ ] SGBD
- [ ] EL

<details><summary>➡️ Voir l'indice</summary>
Reçoit données du client.
</details>

<details><summary>➡️ Voir la réponse</summary>
La **Servlet**.
</details>

---

### ❓ Q11 — Quel est l’ordre correct du flux MVC ?
- [ ] JSP → Servlet → BD → Client
- [ ] Client → JSP → Servlet → Modèle → Client
- [ ] Client → Servlet → Modèle → JSP → Client
- [ ] BD → Servlet → Modèle → JSP

<details><summary>➡️ Voir l'indice</summary>
Du client vers la vue finale.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Client → Servlet → Modèle → JSP → Client**
</details>

---

### ❓ Q12 — Comment une servlet transmet des données à une JSP ?
- [ ] response.redirectData()
- [ ] request.setAttribute()
- [ ] request.save()
- [ ] jsp.setValue()

<details><summary>➡️ Voir l'indice</summary>
Scope requête.
</details>

<details><summary>➡️ Voir la réponse</summary>
`request.setAttribute()`
</details>

---

### ❓ Q13 — Comment une JSP lit un attribut envoyé par la servlet ?
- [ ] ${session.attr}
- [ ] ${requestScope.attr}
- [ ] ${cookie.attr}
- [ ] ${header.attr}

<details><summary>➡️ Voir l'indice</summary>
EL.
</details>

<details><summary>➡️ Voir la réponse</summary>
`${requestScope.attr}`
</details>

---

### ❓ Q14 — Le forward est :
- [ ] Une redirection client
- [ ] Une redirection serveur
- [ ] Une mise en cache
- [ ] Un appel BD

<details><summary>➡️ Voir l'indice</summary>
URL ne change pas.
</details>

<details><summary>➡️ Voir la réponse</summary>
Une **redirection serveur**.
</details>

---

### ❓ Q15 — Le redirect est :
- [ ] Serveur
- [ ] Client
- [ ] BD
- [ ] JSP

<details><summary>➡️ Voir l'indice</summary>
URL change.
</details>

<details><summary>➡️ Voir la réponse</summary>
Une **redirection client**.
</details>

---

### ❓ Q16 — Lors d’un redirect, les données passent via :
- [ ] setAttribute()
- [ ] session
- [ ] paramètres URL
- [ ] cookies uniquement

<details><summary>➡️ Voir l'indice</summary>
Visibles.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Paramètres URL**.
</details>

---

### ❓ Q17 — Avantage du MVC :
- [ ] Plus rapide que JDBC
- [ ] Séparation des responsabilités
- [ ] Réduit la taille des fichiers CSS
- [ ] Supprime les servlets

<details><summary>➡️ Voir l'indice</summary>
Réduction du couplage.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Séparation des responsabilités**.
</details>

---

### ❓ Q18 — Le modèle contient généralement :
- [ ] HTML
- [ ] Le code métier + persistance
- [ ] Du JavaScript
- [ ] Des requêtes HTTP

<details><summary>➡️ Voir l'indice</summary>
JavaBeans.
</details>

<details><summary>➡️ Voir la réponse</summary>
Le **métier** et la **persistance**.
</details>

---

### ❓ Q19 — La JSP doit éviter :
- [ ] L’EL
- [ ] Le HTML
- [ ] Les scriptlets Java
- [ ] L’affichage de données

<details><summary>➡️ Voir l'indice</summary>
Mal pratique, mauvais MVC.
</details>

<details><summary>➡️ Voir la réponse</summary>
Les **scriptlets Java**.
</details>

---

### ❓ Q20 — Le contrôleur gère aussi :
- [ ] Le CSS
- [ ] Les sessions
- [ ] Le stockage disque
- [ ] Les graphismes

<details><summary>➡️ Voir l'indice</summary>
Login, panier.
</details>

<details><summary>➡️ Voir la réponse</summary>
Les **sessions**.
</details>

---

### ❓ Q21 — Une JSP peut-elle accéder directement au modèle ?
- [ ] Oui, via JavaBeans
- [ ] Non, seulement via JS
- [ ] Non, uniquement via BD
- [ ] Non, pas en MVC

<details><summary>➡️ Voir l'indice</summary>
jsp:useBean
</details>

<details><summary>➡️ Voir la réponse</summary>
Oui, via **JavaBeans**.
</details>

---

### ❓ Q22 — Le contrôleur sert aussi à :
- [ ] Décorer le HTML
- [ ] Choisir la vue à afficher
- [ ] Compiler des JSP
- [ ] Créer des cookies

<details><summary>➡️ Voir l'indice</summary>
Rôle d’orchestration.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Choisir la vue**.
</details>

---

### ❓ Q23 — Comment une JSP déclenche une action vers une servlet ?
- [ ] Via CSS
- [ ] Via un `<form>`
- [ ] Via la BD
- [ ] Via une balise EL

<details><summary>➡️ Voir l'indice</summary>
Action="ServletName"
</details>

<details><summary>➡️ Voir la réponse</summary>
Via un **formulaire** vers la servlet.
</details>

---

### ❓ Q24 — Dans MVC, le couplage faible est obtenu car :
- [ ] Le code est mélangé
- [ ] Les rôles sont séparés
- [ ] Les JSP modifient la BD
- [ ] Tout est dans une servlet

<details><summary>➡️ Voir l'indice</summary>
Concept fondamental.
</details>

<details><summary>➡️ Voir la réponse</summary>
Les rôles sont **séparés**.
</details>

---

### ❓ Q25 — Pourquoi MVC facilite les tests ?
- [ ] Le modèle tourne sans interface
- [ ] Les JSP testent automatiquement
- [ ] HTTP fait les tests
- [ ] JDBC teste la vue

<details><summary>➡️ Voir l'indice</summary>
Tester le métier sans HTML.
</details>

<details><summary>➡️ Voir la réponse</summary>
Car on peut tester le **modèle seul**, sans la vue.
</details>

# **5.6. Gestion État & Utilisateurs / JDBC**
### ❓ Q1 — Qu’est-ce qu’un cookie côté Web ?
- [ ] Un fichier exécutable
- [ ] Un petit texte stocké dans le navigateur
- [ ] Un script Java
- [ ] Un objet Java côté serveur

<details><summary>➡️ Voir l'indice</summary>
Stocké côté client.
</details>

<details><summary>➡️ Voir la réponse</summary>
Un **petit fichier texte** stocké dans le navigateur.
</details>

---

### ❓ Q2 — Taille maximale d’un cookie ?
- [ ] 20 Ko
- [ ] 1 Ko
- [ ] 4 Ko
- [ ] 100 Ko

<details><summary>➡️ Voir l'indice</summary>
Limite officielle des navigateurs.
</details>

<details><summary>➡️ Voir la réponse</summary>
**4 Ko**
</details>

---

### ❓ Q3 — Comment une servlet crée un cookie ?
- [ ] new HTTPcookie()
- [ ] new Cookie(nom,valeur)
- [ ] Cookie.create()
- [ ] request.addCookie()

<details><summary>➡️ Voir l'indice</summary>
Objet Java standard.
</details>

<details><summary>➡️ Voir la réponse</summary>
`new Cookie(nom, valeur)`
</details>

---

### ❓ Q4 — Comment une servlet envoie un cookie au client ?
- [ ] request.addCookie()
- [ ] session.attachCookie()
- [ ] response.addCookie()
- [ ] jsp.addCookie()

<details><summary>➡️ Voir l'indice</summary>
Réponse HTTP.
</details>

<details><summary>➡️ Voir la réponse</summary>
`response.addCookie()`
</details>

---

### ❓ Q5 — Comment lit-on les cookies dans une servlet ?
- [ ] response.getCookies()
- [ ] session.getCookies()
- [ ] request.getCookies()
- [ ] request.cookie()

<details><summary>➡️ Voir l'indice</summary>
Requête entrante.
</details>

<details><summary>➡️ Voir la réponse</summary>
`request.getCookies()`
</details>

---

### ❓ Q6 — Les cookies peuvent contenir :
- [ ] Du code exécutable
- [ ] Des virus
- [ ] Un simple texte
- [ ] Un fichier ZIP

<details><summary>➡️ Voir l'indice</summary>
Jamais dangereux en eux-mêmes.
</details>

<details><summary>➡️ Voir la réponse</summary>
Un **texte simple**.
</details>

---

### ❓ Q7 — Quel est le principal risque des cookies ?
- [ ] Infection système
- [ ] Perte de performance
- [ ] Fuite d’informations en clair
- [ ] Crash du serveur

<details><summary>➡️ Voir l'indice</summary>
Pas chiffrés.
</details>

<details><summary>➡️ Voir la réponse</summary>
Une **fuite de données sensibles**.
</details>

---

### ❓ Q8 — Pourquoi HTTP nécessite un mécanisme de session ?
- [ ] HTTP est lent
- [ ] HTTP est sans état
- [ ] HTTP gère mal les cookies
- [ ] HTTP duplique les requêtes

<details><summary>➡️ Voir l'indice</summary>
Stateless.
</details>

<details><summary>➡️ Voir la réponse</summary>
Parce qu’HTTP est **sans état**.
</details>

---

### ❓ Q9 — Comment récupérer une HttpSession ?
- [ ] response.getSession()
- [ ] request.getSession()
- [ ] new Session()
- [ ] jsp:getSession()

<details><summary>➡️ Voir l'indice</summary>
Toujours depuis la requête.
</details>

<details><summary>➡️ Voir la réponse</summary>
`request.getSession()`
</details>

---

### ❓ Q10 — Comment stocker une donnée dans la session ?
- [ ] request.save()
- [ ] session.add()
- [ ] session.setAttribute()
- [ ] response.setSession()

<details><summary>➡️ Voir l'indice</summary>
Panier, login…
</details>

<details><summary>➡️ Voir la réponse</summary>
`session.setAttribute()`
</details>

---

### ❓ Q11 — Comment lire une donnée session ?
- [ ] session.read()
- [ ] session.get()
- [ ] session.getAttribute()
- [ ] request.getSessionData()

<details><summary>➡️ Voir l'indice</summary>
Symétrique de setAttribute.
</details>

<details><summary>➡️ Voir la réponse</summary>
`session.getAttribute()`
</details>

---

### ❓ Q12 — Un champ caché est utilisé pour :
- [ ] Chiffrer les mots de passe
- [ ] Stocker un identifiant dans un formulaire
- [ ] Afficher des messages d’erreur
- [ ] Remplacer une session

<details><summary>➡️ Voir l'indice</summary>
Toujours envoyé avec le formulaire.
</details>

<details><summary>➡️ Voir la réponse</summary>
Stocker un **identifiant discret**.
</details>

---

### ❓ Q13 — Inconvénient des paramètres URL ?
- [ ] Trop rapides
- [ ] Supportés uniquement par Chrome
- [ ] Visibles dans la barre d'adresse
- [ ] Suppriment les cookies

<details><summary>➡️ Voir l'indice</summary>
GET = visible.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Visibles**, peu sécurisés.
</details>

---

### ❓ Q14 — La session est utile pour :
- [ ] Compresser les images
- [ ] Stocker des données utilisateur persistantes
- [ ] Appliquer des styles CSS
- [ ] Compiler des JSP

<details><summary>➡️ Voir l'indice</summary>
Panier, login…
</details>

<details><summary>➡️ Voir la réponse</summary>
**Stocker des données utilisateur**.
</details>

---

### ❓ Q15 — Que signifie autoCommit = false ?
- [ ] Chaque requête SQL s'exécute deux fois
- [ ] On doit appeler commit() manuellement
- [ ] Le SGBD ignore les requêtes
- [ ] JDBC ferme la connexion

<details><summary>➡️ Voir l'indice</summary>
Transactions explicites.
</details>

<details><summary>➡️ Voir la réponse</summary>
On doit appeler **commit** manuellement.
</details>

---

### ❓ Q16 — Quel appel JDBC exécute un SELECT ?
- [ ] executeUpdate()
- [ ] executeQuery()
- [ ] executeSelect()
- [ ] runSQL()

<details><summary>➡️ Voir l'indice</summary>
Retourne un ResultSet.
</details>

<details><summary>➡️ Voir la réponse</summary>
`executeQuery()`
</details>

---

### ❓ Q17 — Quelle méthode JDBC est utilisée pour INSERT / UPDATE / DELETE ?
- [ ] executeQuery()
- [ ] executeInsert()
- [ ] updateRows()
- [ ] executeUpdate()

<details><summary>➡️ Voir l'indice</summary>
Retourne un nombre de lignes modifiées.
</details>

<details><summary>➡️ Voir la réponse</summary>
`executeUpdate()`
</details>

---

### ❓ Q18 — Comment lire une ligne suivante dans un ResultSet ?
- [ ] rs.next()
- [ ] rs.forward()
- [ ] rs.read()
- [ ] rs.step()

<details><summary>➡️ Voir l'indice</summary>
Toujours dans les boucles.
</details>

<details><summary>➡️ Voir la réponse</summary>
`rs.next()`
</details>

---

### ❓ Q19 — Quel objet JDBC représente une connexion BD ?
- [ ] JDBCSession
- [ ] DBLink
- [ ] Connection
- [ ] Connector

<details><summary>➡️ Voir l'indice</summary>
DriverManager le crée.
</details>

<details><summary>➡️ Voir la réponse</summary>
`Connection`
</details>

---

### ❓ Q20 — Comment charger explicitement un driver JDBC ?
- [ ] Driver.load()
- [ ] Class.forName()
- [ ] import jdbc.*
- [ ] JDBC.load()

<details><summary>➡️ Voir l'indice</summary>
Ancienne méthode, toujours enseignée.
</details>

<details><summary>➡️ Voir la réponse</summary>
`Class.forName()`
</details>

---

### ❓ Q21 — Quel objet exécute les requêtes SQL ?
- [ ] SQLRunner
- [ ] ResultSet
- [ ] Statement ou PreparedStatement
- [ ] Connection

<details><summary>➡️ Voir l'indice</summary>
Il existe trois types.
</details>

<details><summary>➡️ Voir la réponse</summary>
`Statement` / `PreparedStatement`
</details>

---

### ❓ Q22 — Quel est l’intérêt d’un PreparedStatement ?
- [ ] Plus lent mais plus simple
- [ ] Évite les injections SQL
- [ ] Remplace la BD
- [ ] Compile du HTML

<details><summary>➡️ Voir l'indice</summary>
Paramètres "?".
</details>

<details><summary>➡️ Voir la réponse</summary>
**Évite les injections SQL** et optimise.
</details>

---

### ❓ Q23 — Comment accéder à une colonne dans un ResultSet ?
- [ ] rs.value()
- [ ] rs.get("col")
- [ ] rs.getXXX("col")
- [ ] rs.column("col")

<details><summary>➡️ Voir l'indice</summary>
XXX = int, String, double…
</details>

<details><summary>➡️ Voir la réponse</summary>
`rs.getXXX("col")`
</details>

---

### ❓ Q24 — À quoi sert DatabaseMetaData ?
- [ ] Lire la structure de la BD
- [ ] Optimiser les queries
- [ ] Gérer les transactions
- [ ] Configurer Tomcat

<details><summary>➡️ Voir l'indice</summary>
Très utile en introspection.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Lire la structure BD**.
</details>

---

### ❓ Q25 — À quoi sert ResultSetMetaData ?
- [ ] Lire le nombre de colonnes
- [ ] Traduire en JSON
- [ ] Écrire dans la BD
- [ ] Chiffrer les données

<details><summary>➡️ Voir l'indice</summary>
Noms, types, compte des colonnes.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Décrire les colonnes du ResultSet.**
</details>

---

### ❓ Q26 — Pourquoi doit-on toujours fermer rs, st et cx ?
- [ ] Pour vider le cache local
- [ ] Pour éviter les fuites de ressources
- [ ] Pour supprimer la table
- [ ] Pour relancer Tomcat

<details><summary>➡️ Voir l'indice</summary>
Très important en JDBC.
</details>

<details><summary>➡️ Voir la réponse</summary>
Éviter les **fuites de ressources**.
</details>

---

### ❓ Q27 — Que fait rollback() ?
- [ ] Valide la transaction
- [ ] Annule la transaction
- [ ] Réinitialise la BD
- [ ] Ferme la connexion

<details><summary>➡️ Voir l'indice</summary>
Opposé de commit.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Annule** la transaction.
</details>

---

### ❓ Q28 — Que permet une transaction JDBC ?
- [ ] Transformer du HTML en Java
- [ ] Regrouper plusieurs requêtes atomiquement
- [ ] Désactiver la BD
- [ ] Créer des cookies

<details><summary>➡️ Voir l'indice</summary>
Tout ou rien.
</details>

<details><summary>➡️ Voir la réponse</summary>
Regrouper plusieurs requêtes **atomiquement**.
</details>

---

### ❓ Q29 — Quel est l’ordre correct d’utilisation JDBC ?
- [ ] Connexion → Fermeture → Requête
- [ ] Driver → Connexion → Statement → SQL → ResultSet → Fermeture
- [ ] SQL → Statement → Connexion
- [ ] ResultSet → Statement → Connexion

<details><summary>➡️ Voir l'indice</summary>
Voir schéma du cours.
</details>

<details><summary>➡️ Voir la réponse</summary>
Driver → Connexion → Statement → SQL → ResultSet → Fermeture
</details>

---

### ❓ Q30 — Un batch JDBC sert à :
- [ ] Exécuter plusieurs requêtes en une fois
- [ ] Compresser les tables
- [ ] Charger le driver automatiquement
- [ ] Écrire dans des JSP

<details><summary>➡️ Voir l'indice</summary>
Optimisation des écritures.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Exécuter plusieurs requêtes en lot.**
</details>



---

# **7. Exceptions en Java**

### ❓ Q1 — Quel est le rôle du bloc try ?
- [ ] Exécuter le code sans exception
- [ ] Encapsuler du code susceptible de lever une exception
- [ ] Fermer automatiquement les ressources
- [ ] Intercepter toutes les erreurs système

<details><summary>➡️ Voir l'indice</summary>
C'est la zone “risquée”.
</details>

<details><summary>➡️ Voir la réponse</summary>
Encapsuler du code **susceptible de lever une exception**.
</details>

---

### ❓ Q2 — Quand s’exécute un bloc catch ?
- [ ] Toujours
- [ ] Jamais
- [ ] Seulement si une exception compatible est levée
- [ ] Avant le try

<details><summary>➡️ Voir l'indice</summary>
Filtrage par type.
</details>

<details><summary>➡️ Voir la réponse</summary>
Seulement si une **exception compatible** est levée.
</details>

---

### ❓ Q3 — Le bloc finally s’exécute :
- [ ] Uniquement si pas d’exception
- [ ] Uniquement si exception
- [ ] Toujours (sauf crash JVM)
- [ ] Une fois par thread

<details><summary>➡️ Voir l'indice</summary>
Idéal pour fermer des flux.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Toujours**, qu'il y ait exception ou non.
</details>

---

### ❓ Q4 — Une exception checked doit être :
- [ ] Ignorée
- [ ] Documentée ou capturée
- [ ] Transformée en erreur système
- [ ] Déclarée dans un fichier XML

<details><summary>➡️ Voir l'indice</summary>
Compiler → obligation.
</details>

<details><summary>➡️ Voir la réponse</summary>
Elle doit être **capturée** ou **déclarée avec throws**.
</details>

---

### ❓ Q5 — Une exception unchecked appartient à :
- [ ] Exception
- [ ] IOException
- [ ] RuntimeException
- [ ] Error

<details><summary>➡️ Voir l'indice</summary>
NullPointerException en fait partie.
</details>

<details><summary>➡️ Voir la réponse</summary>
**RuntimeException**
</details>

---

### ❓ Q6 — Quelle exception est unchecked ?
- [ ] SQLException
- [ ] IOException
- [ ] RuntimeException
- [ ] FileNotFoundException

<details><summary>➡️ Voir l'indice</summary>
Elle n'a pas besoin de throws.
</details>

<details><summary>➡️ Voir la réponse</summary>
**RuntimeException**
</details>

---

### ❓ Q7 — Quel est le rôle de “throws” dans une méthode ?
- [ ] Capter l’exception
- [ ] Déclarer que la méthode peut propager une exception
- [ ] Forcer un catch interne
- [ ] Convertir l’exception en String

<details><summary>➡️ Voir l'indice</summary>
Signature de la méthode.
</details>

<details><summary>➡️ Voir la réponse</summary>
Déclarer que la méthode **peut propager** une exception.
</details>

---

### ❓ Q8 — Quel est le rôle de “throw” ?
- [ ] Documenter une méthode
- [ ] Créer un fichier log
- [ ] Lancer explicitement une exception
- [ ] Réparer l'exception

<details><summary>➡️ Voir l'indice</summary>
Utilisé pour signaler une erreur.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Lancer explicitement** une exception.
</details>

---

### ❓ Q9 — Le try-with-resources permet :
- [ ] D’éviter finally
- [ ] De gérer automatiquement la fermeture des ressources
- [ ] D’exécuter du code en parallèle
- [ ] De supprimer les exceptions

<details><summary>➡️ Voir l'indice</summary>
AutoCloseable.
</details>

<details><summary>➡️ Voir la réponse</summary>
**Fermeture automatique des ressources**.
</details>

---

### ❓ Q10 — Les ressources du try-with-resources doivent implémenter :
- [ ] Runnable
- [ ] Serializable
- [ ] AutoCloseable
- [ ] Closeable uniquement

<details><summary>➡️ Voir l'indice</summary>
close() automatique.
</details>

<details><summary>➡️ Voir la réponse</summary>
`AutoCloseable`
</details>

---

### ❓ Q11 — Quel type d’exception représente un bug du programme ?
- [ ] Checked
- [ ] Unchecked
- [ ] IOException
- [ ] Throwable uniquement

<details><summary>➡️ Voir l'indice</summary>
Souvent NullPointerException.
</details>

<details><summary>➡️ Voir la réponse</summary>
Une **unchecked** (RuntimeException).
</details>

---

### ❓ Q12 — Quelle instruction garantit l’exécution d’un bloc même si return apparaît dans le try ?
- [ ] catch
- [ ] throw
- [ ] finally
- [ ] throws

<details><summary>➡️ Voir l'indice</summary>
Toujours exécuté.
</details>

<details><summary>➡️ Voir la réponse</summary>
`finally`
</details>

---

### ❓ Q13 — Que signifie la propagation d’une exception ?
- [ ] L’exception disparaît
- [ ] L’exception remonte à l’appelant
- [ ] La JVM se ferme
- [ ] Le programme redémarre

<details><summary>➡️ Voir l'indice</summary>
Appels imbriqués.
</details>

<details><summary>➡️ Voir la réponse</summary>
L’exception **remonte** à la méthode appelante.
</details>

---

### ❓ Q14 — Que se passe-t-il si aucune méthode ne capture une exception ?
- [ ] Le programme continue normalement
- [ ] La JVM la capture automatiquement
- [ ] Le programme s’arrête
- [ ] Elle se transforme en warning

<details><summary>➡️ Voir l'indice</summary>
Stacktrace.
</details>

<details><summary>➡️ Voir la réponse</summary>
Le programme **s’arrête** (exception non gérée).
</details>

---

### ❓ Q15 — Quelle est la structure correcte d’un try-with-resources ?
- [ ] try {Resource} catch {}
- [ ] try Resource(resource) {}
- [ ] try (Resource r = new Resource()) {}
- [ ] try new Resource() {}

<details><summary>➡️ Voir l'indice</summary>
Parenthèses obligatoires.
</details>

<details><summary>➡️ Voir la réponse</summary>
`try (Resource r = new Resource()) {}`
</details>

---

# **8. ORM, JPA & Hibernate**
### ❓ Q1 — À quoi sert un ORM ?
- [ ] Générer des pages HTML
- [ ] Faire le mapping objets ↔ tables BD
- [ ] Compiler du Java
- [ ] Exécuter CSS

<details><summary>➡️ Indice</summary>
Évite d'écrire du SQL à la main.
</details>

<details><summary>➡️ Réponse</summary>
À réaliser le **mapping objet-relationnel**.
</details>

---

### ❓ Q2 — Pourquoi un ORM facilite-t-il le développement ?
- [ ] La BD devient inutile
- [ ] On travaille avec des objets plutôt qu’avec du SQL brut
- [ ] Il supprime les exceptions Java
- [ ] Il remplace JDBC

<details><summary>➡️ Indice</summary>
C’est le but même d’Hibernate.
</details>

<details><summary>➡️ Réponse</summary>
Parce qu’on **manipule des objets**, pas du SQL brut.
</details>

---

### ❓ Q3 — Quel problème un ORM résout-il concernant les références objet ?
- [ ] La compilation
- [ ] Les relations unidirectionnelles vs bidirectionnelles BD
- [ ] Le tri des listes
- [ ] Le formatage des dates

<details><summary>➡️ Indice</summary>
Objets ≠ tables.
</details>

<details><summary>➡️ Réponse</summary>
Les **références objet ↔ relations BD**.
</details>

---

### ❓ Q4 — Un ORM inclut un mécanisme de cache pour :
- [ ] Accélérer l’affichage HTML
- [ ] Éviter que deux objets représentant la même ligne BD coexistent
- [ ] Réduire la mémoire Java
- [ ] Désactiver JDBC

<details><summary>➡️ Indice</summary>
Objet unique ↔ tuple unique.
</details>

<details><summary>➡️ Réponse</summary>
Éviter la **duplication d’objets** pour une même ligne BD.
</details>

---

### ❓ Q5 — JPA est :
- [ ] Un framework
- [ ] Une spécification
- [ ] Une base de données
- [ ] Une extension du CSS

<details><summary>➡️ Indice</summary>
Hibernate en est une implémentation.
</details>

<details><summary>➡️ Réponse</summary>
Une **spécification**.
</details>

---

### ❓ Q6 — Hibernate est :
- [ ] Une base SQL
- [ ] Une implémentation de JPA
- [ ] Une API réseau
- [ ] Un serveur web

<details><summary>➡️ Indice</summary>
Mapping + annotations.
</details>

<details><summary>➡️ Réponse</summary>
Une **implémentation JPA**.
</details>

---

### ❓ Q7 — À quoi servent les annotations dans Hibernate ?
- [ ] Styliser le code
- [ ] Décrire le mapping BD (colonnes, tables, PK…)
- [ ] Exécuter du SQL natif uniquement
- [ ] Définir des CSS

<details><summary>➡️ Indice</summary>
@Entity, @Id, @OneToMany …
</details>

<details><summary>➡️ Réponse</summary>
À **définir le mapping BD** directement dans les classes.
</details>

---

### ❓ Q8 — Que représente l’état “éphémère” ?
- [ ] Objet lié à une session Hibernate
- [ ] Objet créé avec new et non encore stocké
- [ ] Objet supprimé
- [ ] Objet jamais instancié

<details><summary>➡️ Indice</summary>
Pas encore en BD.
</details>

<details><summary>➡️ Réponse</summary>
Objet **créé par new**, sans ID persisté.
</details>

---

### ❓ Q9 — Un objet persistant est :
- [ ] Dans une session Hibernate
- [ ] Converti en JSON
- [ ] Un cookie
- [ ] Sériel

<details><summary>➡️ Indice</summary>
update auto.
</details>

<details><summary>➡️ Réponse</summary>
Un objet **attaché à une session**.
</details>

---

### ❓ Q10 — Un objet détaché :
- [ ] Est supprimé de la BD
- [ ] Était persistant mais session fermée
- [ ] Est un cookie
- [ ] Est un PreparedStatement

<details><summary>➡️ Indice</summary>
Plus dans le cache.
</details>

<details><summary>➡️ Réponse</summary>
Il **provient d’une session fermée**.
</details>

---

### ❓ Q11 — Quelle méthode rend persistant un objet éphémère ?
- [ ] remove()
- [ ] update()
- [ ] save() / persist()
- [ ] drop()

<details><summary>➡️ Indice</summary>
Insertion en BD.
</details>

<details><summary>➡️ Réponse</summary>
`save()` / `persist()`.
</details>

---

### ❓ Q12 — Quelle méthode réattache un objet détaché ?
- [ ] merge()
- [ ] delete()
- [ ] close()
- [ ] drop()

<details><summary>➡️ Indice</summary>
Fusionne états détachés.
</details>

<details><summary>➡️ Réponse</summary>
`merge()`
</details>

---

### ❓ Q13 — Quelle méthode détache un objet persistant ?
- [ ] evict()
- [ ] remove()
- [ ] save()
- [ ] persist()

<details><summary>➡️ Indice</summary>
Enlève du cache.
</details>

<details><summary>➡️ Réponse</summary>
`evict()`
</details>

---

### ❓ Q14 — Différence get() vs load() ?
- [ ] load est plus lent
- [ ] load renvoie un proxy et charge tardivement
- [ ] get renvoie un proxy
- [ ] get échoue toujours

<details><summary>➡️ Indice</summary>
Lazy loading.
</details>

<details><summary>➡️ Réponse</summary>
`load()` crée un **proxy** (lazy), `get()` charge **immédiatement**.
</details>

---

### ❓ Q15 — Quel langage de requêtes utilise Hibernate ?
- [ ] HQL
- [ ] CSS
- [ ] HTML
- [ ] JDBC

<details><summary>➡️ Indice</summary>
Basé objets, pas tables.
</details>

<details><summary>➡️ Réponse</summary>
**HQL**
</details>

---

### ❓ Q16 — Quel type de requêtes évite les injections SQL ?
- [ ] SQL natif
- [ ] HQL pur
- [ ] Criteria API
- [ ] String.split()

<details><summary>➡️ Indice</summary>
API objet.
</details>

<details><summary>➡️ Réponse</summary>
**Criteria API**
</details>

---

### ❓ Q17 — Une association one-to-many représente :
- [ ] A → B (plusieurs)
- [ ] B → A (un)
- [ ] A → plusieurs B
- [ ] Plusieurs BD

<details><summary>➡️ Indice</summary>
Collection.
</details>

<details><summary>➡️ Réponse</summary>
**Un A → plusieurs B**.
</details>

---

### ❓ Q18 — One-to-many se mappe via :
- [ ] @OneToOne
- [ ] @ManyToOne côté “many”, @OneToMany côté “one”
- [ ] @JoinTable uniquement
- [ ] @EntityOnly

<details><summary>➡️ Indice</summary>
Toujours deux côtés.
</details>

<details><summary>➡️ Réponse</summary>
@ManyToOne + @OneToMany
</details>

---

### ❓ Q19 — Une association many-to-many nécessite :
- [ ] Deux colonnes simples
- [ ] Une table de jointure
- [ ] Un cookie
- [ ] Une JSP

<details><summary>➡️ Indice</summary>
Cas classique étudiant/cours.
</details>

<details><summary>➡️ Réponse</summary>
Une **table de jointure**.
</details>

---

### ❓ Q20 — Une classe d’association est nécessaire lorsqu’une relation many-to-many :
- [ ] A des attributs propres
- [ ] Contient du HTML
- [ ] Est un simple Set
- [ ] Est lazy

<details><summary>➡️ Indice</summary>
Table "Valider" dans le cours.
</details>

<details><summary>➡️ Réponse</summary>
Quand la relation **a ses propres attributs**.
</details>

---

### ❓ Q21 — Un ID composite en Hibernate utilise :
- [ ] @IdOnly
- [ ] Une classe Embeddable + EmbeddedId
- [ ] Trois colonnes obligatoires
- [ ] Un cookie

<details><summary>➡️ Indice</summary>
Deux classes.
</details>

<details><summary>➡️ Réponse</summary>
**EmbeddedId + classe @Embeddable**
</details>

---

### ❓ Q22 — L’héritage SINGLE_TABLE implique :
- [ ] Plusieurs tables
- [ ] Une seule table pour toute la hiérarchie
- [ ] Aucune table
- [ ] Un fichier XML

<details><summary>➡️ Indice</summary>
Colonne discriminante.
</details>

<details><summary>➡️ Réponse</summary>
**Une seule table**.
</details>

---

### ❓ Q23 — Avantage de SINGLE_TABLE ?
- [ ] Très lent
- [ ] Pas de jointures → très rapide
- [ ] Multi-BD
- [ ] Supprime JDBC

<details><summary>➡️ Indice</summary>
Performance.
</details>

<details><summary>➡️ Réponse</summary>
**Pas de jointures**, donc rapide.
</details>

---

### ❓ Q24 — Défaut de SINGLE_TABLE ?
- [ ] Trop de jointures
- [ ] Beaucoup de valeurs nulles
- [ ] Trop lent
- [ ] Incompatible Java

<details><summary>➡️ Indice</summary>
Colonnes inutiles.
</details>

<details><summary>➡️ Réponse</summary>
**Beaucoup de valeurs NULL**.
</details>

---

### ❓ Q25 — L’héritage JOINED implique :
- [ ] Une table unique
- [ ] Une table par classe avec jointures
- [ ] Aucun lien
- [ ] Une seule colonne

<details><summary>➡️ Indice</summary>
Plus OO.
</details>

<details><summary>➡️ Réponse</summary>
Une table **par classe**, jointures.
</details>

---

### ❓ Q26 — Avantage du JOINED :
- [ ] Plus proche du modèle objet
- [ ] Plus rapide
- [ ] Supprime JDBC
- [ ] Pas de clé primaire

<details><summary>➡️ Indice</summary>
Fidèle au modèle.
</details>

<details><summary>➡️ Réponse</summary>
**Modélisation fidèle**.
</details>

---

### ❓ Q27 — Défaut du JOINED :
- [ ] Trop simple
- [ ] Jointures lourdes et plus lentes
- [ ] Interdit les clés composites
- [ ] Supprime HQL

<details><summary>➡️ Indice</summary>
Performance.
</details>

<details><summary>➡️ Réponse</summary>
Jointures **plus lentes**.
</details>

---

### ❓ Q28 — TABLE_PER_CLASS signifie :
- [ ] Une table unique
- [ ] Une table par classe concrète
- [ ] Une table par attribut
- [ ] Une table par annotation

<details><summary>➡️ Indice</summary>
Les classes abstraites n’ont pas de table.
</details>

<details><summary>➡️ Réponse</summary>
Une **table par classe concrète**.
</details>

---

### ❓ Q29 — Défaut de TABLE_PER_CLASS ?
- [ ] Trop rapide
- [ ] Pas de jointure
- [ ] Requêtes polymorphiques complexes
- [ ] Supprime SQL

<details><summary>➡️ Indice</summary>
Union de tables.
</details>

<details><summary>➡️ Réponse</summary>
**Requêtes polymorphiques compliquées**.
</details>

---

### ❓ Q30 — Avantage de TABLE_PER_CLASS ?
- [ ] Structure très simple
- [ ] Pas de colonnes nulles
- [ ] BD automatique
- [ ] Mapping difficile

<details><summary>➡️ Indice</summary>
Comparaison avec SINGLE_TABLE.
</details>

<details><summary>➡️ Réponse</summary>
Pas de **colonnes nulles**.
</details>

---

### ❓ Q31 — Qu’est-ce que HQL exprime ?
- [ ] Les tables BD
- [ ] Les classes et propriétés Java
- [ ] Le HTML des JSP
- [ ] Les fichiers XML

<details><summary>➡️ Indice</summary>
Objet, pas relationnel.
</details>

<details><summary>➡️ Réponse</summary>
Les **classes et propriétés Java**.
</details>

---

### ❓ Q32 — Pourquoi Hibernate utilise-t-il des proxys ?
- [ ] Pour rendre le code plus lent
- [ ] Pour gérer le lazy loading
- [ ] Pour remplacer JDBC
- [ ] Pour exécuter du CSS

<details><summary>➡️ Indice</summary>
load().
</details>

<details><summary>➡️ Réponse</summary>
Pour le **lazy loading**.
</details>

---

### ❓ Q33 — Quand un objet persistant est-il synchronisé avec la BD ?
- [ ] À chaque affectation
- [ ] Au commit ou flush()
- [ ] Quand load() est appelé
- [ ] Jamais

<details><summary>➡️ Indice</summary>
Transaction.
</details>

<details><summary>➡️ Réponse</summary>
Au **commit** ou via **flush()**.
</details>

---

### ❓ Q34 — Une collection @OneToMany est souvent :
- [ ] Un Map obligatoire
- [ ] Un Set ou List
- [ ] Un tableau primitif
- [ ] Un cookie

<details><summary>➡️ Indice</summary>
Recommandations Hibernate.
</details>

<details><summary>➡️ Réponse</summary>
Un **Set ou List**.
</details>

---

### ❓ Q35 — Quelle méthode supprime un objet persistant de la BD ?
- [ ] save()
- [ ] delete() / remove()
- [ ] evict()
- [ ] merge()

<details><summary>➡️ Indice</summary>
Suppression.
</details>

<details><summary>➡️ Réponse</summary>
`delete()` / `remove()`
</details>

---

### ❓ Q36 — Problème classique du lazy loading ?
- [ ] Trop de colonnes
- [ ] Exception LazyInitializationException
- [ ] Trop rapide
- [ ] Incompatible Java

<details><summary>➡️ Indice</summary>
Session fermée.
</details>

<details><summary>➡️ Réponse</summary>
**LazyInitializationException**
</details>

---

### ❓ Q37 — Dans une relation bidirectionnelle, la gestion du propriétaire se fait via :
- [ ] mappedBy
- [ ] owner=true
- [ ] master=true
- [ ] root=true

<details><summary>➡️ Indice</summary>
Côté inverse.
</details>

<details><summary>➡️ Réponse</summary>
`mappedBy`
</details>

---

### ❓ Q38 — Pourquoi créer une classe Embeddable ?
- [ ] Remplacer un bean
- [ ] Déclarer un ID composite
- [ ] Écrire du HTML
- [ ] Gérer JDBC

<details><summary>➡️ Indice</summary>
Plusieurs colonnes.
</details>

<details><summary>➡️ Réponse</summary>
Pour gérer un **ID composite**.
</details>

---

### ❓ Q39 — Quelle est la différence entre persist() et merge() ?
- [ ] persist insère, merge réattache ou met à jour
- [ ] merge supprime l'objet
- [ ] persist supprime l'objet
- [ ] aucune

<details><summary>➡️ Indice</summary>
Détaché vs nouveau.
</details>

<details><summary>➡️ Réponse</summary>
`persist()` insère, `merge()` **réattache / met à jour**.
</details>

---

### ❓ Q40 — Pourquoi un ORM sépare persistance et logique métier ?
- [ ] Pour complexifier
- [ ] Pour respecter MVC et éviter dépendance BD dans métier
- [ ] Pour supprimer les exceptions
- [ ] Pour générer du HTML

<details><summary>➡️ Indice</summary>
Séparation des couches.
</details>

<details><summary>➡️ Réponse</summary>
Pour **séparer métier et accès BD**, cohérent avec MVC.
</details>


---

# **9. DAO & Persistance**

### ❓ Q1 — Quel est le principe fondamental du pattern DAO ?
- [ ] Mélanger logique métier et BD
- [ ] Une classe Java correspond à une table BD
- [ ] Utiliser uniquement du SQL natif
- [ ] Créer des interfaces graphiques

<details><summary>➡️ Indice</summary>
Mapping structurel.
</details>

<details><summary>➡️ Réponse</summary>
**1 classe ↔ 1 table**.
</details>

---

### ❓ Q2 — Que signifie CRUD dans un DAO ?
- [ ] Create, Render, Upload, Delete
- [ ] Create, Read, Update, Delete
- [ ] Copy, Run, Undo, Deploy
- [ ] Aucun

<details><summary>➡️ Indice</summary>
Les 4 opérations principales.
</details>

<details><summary>➡️ Réponse</summary>
**Create, Read, Update, Delete**
</details>

---

### ❓ Q3 — À quoi sert la couche DAO ?
- [ ] Afficher les vues JSP
- [ ] Connecter la couche métier à la BD
- [ ] Compiler le projet
- [ ] Gérer les cookies

<details><summary>➡️ Indice</summary>
Isolation BD.
</details>

<details><summary>➡️ Réponse</summary>
Relier **métier ↔ BD**.
</details>

---

### ❓ Q4 — Une classe persistante doit être un :
- [ ] Thread
- [ ] POJO
- [ ] Cookie
- [ ] Servlet

<details><summary>➡️ Indice</summary>
Plain Old Java Object.
</details>

<details><summary>➡️ Réponse</summary>
Un **POJO**.
</details>

---

### ❓ Q5 — Quel élément est obligatoire dans une classe persistante ?
- [ ] Un constructeur privé
- [ ] Un constructeur vide (public)
- [ ] Une méthode static
- [ ] Un main()

<details><summary>➡️ Indice</summary>
Utilisé par Hibernate.
</details>

<details><summary>➡️ Réponse</summary>
Un **constructeur vide**.
</details>

---

### ❓ Q6 — Pourquoi une classe persistante doit-elle avoir des getters/setters ?
- [ ] Pour le débogage
- [ ] Pour permettre au framework de lire/écrire les champs
- [ ] Pour compiler plus vite
- [ ] Pour générer HTML

<details><summary>➡️ Indice</summary>
Reflection.
</details>

<details><summary>➡️ Réponse</summary>
Pour permettre au framework d’**accéder aux attributs**.
</details>

---

### ❓ Q7 — Quel attribut doit toujours exister dans une classe persistante ?
- [ ] cookie
- [ ] id
- [ ] url
- [ ] session

<details><summary>➡️ Indice</summary>
Identifiant unique.
</details>

<details><summary>➡️ Réponse</summary>
L’**ID**.
</details>

---

### ❓ Q8 — Pourquoi redéfinir equals() et hashCode() ?
- [ ] Pour accélérer JDBC
- [ ] Pour éviter les doublons dans Set / Map
- [ ] Pour générer du HTML
- [ ] Pour trier les cookies

<details><summary>➡️ Indice</summary>
Collections Java.
</details>

<details><summary>➡️ Réponse</summary>
Pour assurer le **bon fonctionnement dans Set/Map**.
</details>

---

### ❓ Q9 — Dans un DAO, quelle méthode réalise la lecture BD ?
- [ ] write()
- [ ] load()
- [ ] find() / getById()
- [ ] select()

<details><summary>➡️ Indice</summary>
Consultation.
</details>

<details><summary>➡️ Réponse</summary>
`find()` ou `getById()`.
</details>

---

### ❓ Q10 — Dans un DAO, la méthode create() correspond à :
- [ ] DELETE
- [ ] INSERT
- [ ] UPDATE
- [ ] SELECT

<details><summary>➡️ Indice</summary>
Ajout d'un tuple.
</details>

<details><summary>➡️ Réponse</summary>
**INSERT**
</details>

---

### ❓ Q11 — Pourquoi séparer DAO et métier ?
- [ ] Pour améliorer le design MVC
- [ ] Pour écrire moins de HTML
- [ ] Pour supprimer les transactions BD
- [ ] Pour compiler plus vite

<details><summary>➡️ Indice</summary>
Couplage.
</details>

<details><summary>➡️ Réponse</summary>
Pour **séparer logique métier et persistance**.
</details>

---

### ❓ Q12 — Une classe DAO accède principalement à :
- [ ] La BD
- [ ] Les JSP
- [ ] Les cookies
- [ ] Les sessions

<details><summary>➡️ Indice</summary>
CRUD.
</details>

<details><summary>➡️ Réponse</summary>
À la **BD**.
</details>

---

### ❓ Q13 — Une classe métier doit :
- [ ] Connaître JDBC
- [ ] Ne pas connaître la BD ni SQL
- [ ] Gérer les JSP
- [ ] Lire les cookies

<details><summary>➡️ Indice</summary>
Pas de SQL dans métier.
</details>

<details><summary>➡️ Réponse</summary>
Elle **ne doit pas connaître la BD**.
</details>

---

### ❓ Q14 — Le rôle d’un DAO est souvent implémenté par :
- [ ] Un fichier XML
- [ ] Une interface + classe d’implémentation
- [ ] Une JSP
- [ ] Un cookie

<details><summary>➡️ Indice</summary>
Bonne pratique.
</details>

<details><summary>➡️ Réponse</summary>
**Interface + implémentation**.
</details>

---

### ❓ Q15 — Une classe persistante ne doit PAS contenir :
- [ ] Des getters/setters
- [ ] Le code métier complexe
- [ ] Un ID
- [ ] Un constructeur vide

<details><summary>➡️ Indice</summary>
Séparation claire.
</details>

<details><summary>➡️ Réponse</summary>
Elle ne doit pas contenir du **métier complexe**.
</details>

---

### ❓ Q16 — Quel est l’avantage principal d’un DAO ?
- [ ] Remplace Hibernate
- [ ] Permet de changer de BD sans toucher au métier
- [ ] Supprime JVM
- [ ] Ajoute des sessions HTTP

<details><summary>➡️ Indice</summary>
Abstraction.
</details>

<details><summary>➡️ Réponse</summary>
Permet de **changer de BD sans toucher au métier**.
</details>

---

### ❓ Q17 — Une classe persistante appartient à quelle couche ?
- [ ] Vue
- [ ] DAO
- [ ] Modèle métier
- [ ] Serveur Tomcat

<details><summary>➡️ Indice</summary>
Ex : Employe, Demande…
</details>

<details><summary>➡️ Réponse</summary>
À la **couche métier (modèle)**.
</details>

---

### ❓ Q18 — Dans une classe persistante, equals() doit comparer :
- [ ] Les cookies du navigateur
- [ ] Tous les attributs sauf l’ID
- [ ] L’ID uniquement (souvent)
- [ ] L’adresse mémoire

<details><summary>➡️ Indice</summary>
Identité en BD.
</details>

<details><summary>➡️ Réponse</summary>
**L’ID** (selon bonne pratique ORM).
</details>

---

### ❓ Q19 — Une classe persistante doit être :
- [ ] Serializable
- [ ] Final
- [ ] Abstraite
- [ ] Un thread

<details><summary>➡️ Indice</summary>
Nécessaire pour certains frameworks.
</details>

<details><summary>➡️ Réponse</summary>
**Serializable** est recommandé.
</details>

---

### ❓ Q20 — Pourquoi lier DAO et POJO ?
- [ ] Pour exécuter des JSP plus vite
- [ ] Pour transformer une ligne BD en objet Java cohérent
- [ ] Pour créer des API REST
- [ ] Pour gérer les cookies

<details><summary>➡️ Indice</summary>
Mapping BD → objet.
</details>

<details><summary>➡️ Réponse</summary>
Pour **convertir un tuple BD en objet métier**.
</details>


---

# **10. Schémas à maîtriser

### MVC global

### Cycle requête HTTP

### Cycle de vie Servlet

### Fonctionnement JSP

### JDBC workflow

### États Hibernate

### Associations ORM

Tu veux que je te génère **tous les schémas Mermaid impeccables pour l’apprentissage** ?