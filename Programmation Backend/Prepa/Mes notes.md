---
tags:
  - back
  - exam
---
## Architectures 

#### 1-tiers : Tout est sur le serveur , simple et centralisé 
![[Pasted image 20251127141857.png]]

**Plus** : Admin simple et données centralisées
**Moins** : Montée en charge
#### 2 tiers : Client et serveur de données 
Client (pres et traitement) ; Serveur (gestion des données)
![[Pasted image 20251127142139.png]]
**plus** : Interface plus riche ; Application sur le poste client 
**moins** : Client très sollicité (lourd) ; Dialogue avec serveur trop important, maintenance difficile , Difficulté d'évolution

#### 3 tiers : Client , serveur d'application et serveur de données 

![[Pasted image 20251127145706.png]]
**Client** : gère la presentation
**serveur d'application** : gère les traitements
**serveur de données** : Acceuille la SGBD

##### Plus : 
Les 3 niveaux sont independants , possibilité d'implation sur differentes machines , et evolution plus faciles 

#### n tiers : 
##### Exemple : 
Serveur HTML + moteur de Servvlets
Repartition de la logique application dans des objets metiers 

**plus** : Evolution facile , Montée en charge 
**Moins** : complexité du système et couts elevés de mise en oeuvre

### Le schémat du Gartner group

![[Pasted image 20251127142509.png]]

Differentes Structure que peut avoir l'archi repartie du bakcend 

### Standarts internet 
#### Html : 
Description des pages WEB , Texte + Balises
#### HTTP : 
Protocole d'echange d'information sur les WEB entre client et serveur 
- GET : Charger documents, bianires ou fichiers
- POST : Envoyer ddes infos au serveur 
- PUT : Deposer des documents sur le serveur 
- DELETE : Effacer des documents 
- TRACE : Traccer les requetes 
#### TCP/IP
- Protocole de communication reseau
- IP se charge du routage des infos 
- TCP se charge du controle des données transmises
#### CGI 
- Langage de script 
- Interface entre executable et serveur HTTP


## Client lourd léger et riche 
### Client lourd 
*Applications de bureau*
- S'installe sur le poste client 
- Maintenance et MaJ à la charge de l'utilisateur 
- Dépendance du système d'exploitation
- Utilise les ressources internes
- Interfaces et interacctions riches
- Mode déconnecté 
### Client léger 
*Appli web*
Inverse du client lourd

### Client riche 
- Interface et interactions riches 
- Travail en mode connécté / non connecté 


## Fonctionnement des requêtes HTTP et Dynamique
### Dynamique 
### Coté client 
- Page animée 
- Programme exécuté par le client de façon dynamique 
- Se fait par **programmation** Javaccript
	- Augmente l'interactivité et fait des controle sur des elements des formulaires pour diminuer le dialogue entre client et serveur 
#### Coté serveur 
- Page crée dynamiquement ou statique par un programme executé sur le serveur 
- Recuperation et gestion des infos transmises par le client à des fins de calcul ou de stockage BD
- Generation dynamique de page (fichiers HTML source generés ou resultats d'interogation de BD)

### Requetes HTTP
![[Pasted image 20251127151338.png]]

1. Saisie des données par le User dans le client 
2. Controles locaux dans le client (JS)
3. Envoi de la requête HTTP
4. Execution de la requete dans le serveur d'application
5. Requête potentielle vers la BD
6. Construction et envoi de reponse

- La saisie des infos se fait majoritairement grace à un formulaire + controle de saisie JS 
- la requete envoyée contient l'URL de la resource distant + informations de saisie de l'utilisateur 
- Le serveur WEB analyse la requète en fonction de l'extentions du fichier / repertoire/ nom d'appli
- Ce dernier charge l'environement d'execution puis execute la requete
## Servlets 
C'est des classes JAVA presentes dans le serveur d'application,  permettant de construire des pages dynamiques , sans interface graphique elle peut lire sur le disque du serveur 
### **plus** : 
- Portabilité (étant en JAVA language objet compilé) ; 
- permet l'association avec de nombreux serveurs WEB ; 
- Rapidité grace à la peersistance en memoire après instanciation , permets le multithreading
- Gere facilement les cookies 
- Permets des mecanismes puissants et poussés : 
	- Filtrage
	- Chainage
	- Partage de données entre servlets
### Fonctionnement 
![[Pasted image 20251127161131.png]]
1. Le client fait une requete HTTP
2. Cette dderniere est envoyée au serveur WEB 
3. La servlet s'execute
4. Retour du flot de sortie vers le serveur WEB 
5. Flot transferé depuis le serveur WEB au client
#### Cycle de vie de la servlet 
- Chargement au demarage ou à l'expression de besoin
- initialisation *init* : Initialisation des variables d'instance
- Rechargement
- Execution : reception de la requete et execution de ccette dernière
- Destruction *destroy* 
La Servlet definit necessairement doPost ou doGet selon le type d'envoi de requête

#### HttpServletResponse
- Metadata transmise par le client : Methode, le header, le nom du serveur etc ...
## Les JSP

Code Java inclut dans les pages HTML pour faciliter la prise en charge des aspects statiques

### Fonctionement 

1. le serveur reçoit la JSP
2. Le moteur transforme la JSP en Java qui lui contient une servlet 
3. le servlet est chargé et executé 
4. le flot de retour revient de la servlet au moteur 
5. Le flot est ensuite transmis au serveur WEB
Pour chaque JSP les objets accessibles :
- les request 
- les response
- les sessions
- l'application
- La config de servlet

## MVC 
### Modèle 
JavaBean , Objet simple (attributs+getter/setters), il stocke l'etat des données
### Controleur 
Servlets : Reçoit les requetes HTTP , orchestre en créant / replissant des objets metiers , et gère la session

### Vue 
JSP : Accès aux objets metier et affichage des resultats, interaction utilisateur 

## Delegation Servlet / JSP

Servelt -> JSP  : Affichage
Servlet -> Servlet 
### Deux façon d'implementer 
#### Chainage : 
Delegation coté Serveur -> Serveur (non vue par l'utilisateur)
#### Redirection
Delegation coté Serveur -> Client (vue par l'user (changement d'URL))

## JDBC
un API permettant d'interagir avec l'importe quel SGBD relationelle par l'intermediaire d'SQL
 c'est un ensemble d'interface decrivant comment interagir avec une BD
 ![[Pasted image 20251127165234.png]]
### Etapes d'implementation 
1. On charge le driver par la JVM
2. On ouvre la connection avvec la BD
3. On crée l'espace d'exxecution de la requete puis on envoie la requete
4. On recupere le resultat 
### Transactions : 
un ensemble de requetes indivisibles 

## Les cookies
Ensemble d'informations envoyées par le servveur et stockées coté client dans le navigateur 
### Utilité 
- Gestion des parametres d'utilisateur 
- Saisie automatique de logins
- Etat de visite 
- Pas de transmition virus possible mais informations ecrites non encodées 
On peut creer, deposer, lire les cookies depuis un servlet 

## Suivi de session
Le protocole HTTP est deconnécté, il ne permets pas la persitance de connecction , les requetes ne sont pas liées et le serveur ne sais pas si une sequence de requetes provient du meme client , c'est donc un problème pour les logins et les formulaires multi etapes

Il est donc necessaire de mettre en place un mecanisme de suivi de session , pour certaines applis il faur retenir des information ddiverses noms , ids , choix etc 
### Solutions 
Il existe diverses solution :
- Stocker dans des cookies , en stockant les IDs dans le navigatuer mais c'est lourd et peu flexible 
- Stocker dans l'url mais tout est visible (securité zero et la chaine est trop longue et peut casser)
- Stocker dans l'HTML , mais c'est peu securisé car visible dans le code source
##### Best solution
- Créer un objet HttpSession dans le serveur cet objet est associé à un seul utilisateur , il persiste dans toutes les pages peut contenir n'importe quoi , est securisé et est crée automatiquement 
- Fonctionement :
	- Le serveur crée une session
	- Il lui assigne un id de session
	- Le navigateur renvoie ce token à chaque requete via cookie
	- Le serveur reconnait ou pas l'utilisateur 
	- La session garde toutes ses données
- Utilisation :
	- getSession(true) crée la session
	- getSession(false) retourne le nom de la session si elle n'existe pas 
	- setAttribute("nom",Objet) stocke l'objet dans la ssession
	- getAttribute("nom") get l'objet

## Exceptions
Evenement qui intervient pendant l'execution d'un programme et interomp l'execution normale de ce dernier 
Doit etre traité car sinon :
- Terminaison anormale du programme
- Ressources non libérées
### Mecanisme de reccuperaton d'exceptions
Evite une terminaison anormale et permets de traiter l'erreur 
##### Avantages
Separation entre le code du programme et le code de gestion d'erreur , regroupement en type d'erreru et propagation à la methode appelante

### Clauses : 
Try : encapsule la partie du code susceptible de generer une erreur 
catch : après le Try , encapsule le traitement associé à l'exception
**Plusieurs catchs possibles par Try**
Finally : Liberer les ressources 
**depuis Java 7 on peut faire un try avec buffer reader afin d'eviter de faire un finally et liberer les ressources quand meme**


## Mappin Objet-Relationel avec hibernate
### Persistance des données 
Technique en charge de l'enregistrement et restauration des données dans une BD , ça permets de garder la donnée après arret du programme

### Pattern DAO (Data access Object)
La couche DAO effectue le lien entre la couche metier et la couche données :
Classes <-> Tbales 
Objets <-> Tuples
Propriété <-> Attribut
Type JAVA <-> Type SQL

Implemente les operations CRUD

### JPA 
C'est un surcouche de JDBC qui utilise des annotaions comme @Entity , @Id @Column , permets de definir les regles  , implementée par Hibernate, permets d'avoir moins de SQL , augmenter la prodctivité et generation automatique

### Problème du mapping 
Quand on fait de l'ORM on peut tomber sur plusieurs problèmes :
- Les relations BD sont bidirectionelle mais les objets ne le sont pas forcement 
- Il faut un tuple par objet pour eviter les incoherences en cas de modification il ne faut pas avoir deux objets pointant sur le meme tuple -> Solution avoir une memoire cache 
- Lors de la creation d'un nouvel objet il faut pouvoir suivre son etat 
	- Ephemere
		- Créé avec new et pas dans la base
	- persistant
		- A été attaché à la session hibernate
	- detaché
		- Object existant dans la base mais session fermée peut etre reataché après  

### Hibernate
Un framework qui applique ORM
Il permet de 
- Manipuler des Objets au lieu de requeter en SQL 
- Gerer les caches
- gerer les transactions 
- Faire du mapping via XML ou annotations @

#### Classe persistante 

C'est une classe java normale ou :
- On a un constructeur vide
- a des getters/setters
- a une annotation @ID et potentiellement @GeneratedValue 
- a equals() et hashCode() pour savoir s deux objets representent la meme ligne et permettre un mapping correct
- Des collections 
	- 1->n : Set
	- n->1 : Une reference suffit
	- n->n : Set ou liste si l'ordre est important 
	- Map : Si la classe d'association Contient des info supplementaires


#### Associations
One-to-many : Collection dans le coté One et ref dans le coté to many
Many-to-Many : Table d'associassion generée automatiquement

#### Heeritage 
On utilise Inheritence dans la classe père @Inheritence(strategy: InheritenceType.TABLE_PER_CLASS, SINGLE_TABLE ou JOINED)