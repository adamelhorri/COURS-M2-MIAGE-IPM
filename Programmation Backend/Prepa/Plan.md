
# **1. Architectures & Web Basics**

## 1.1 Architectures

- 1-tier
    
- 2-tiers
    
- 3-tiers
    
- n-tiers
    
- Types de clients (léger, lourd, riche)
    

## 1.2 Standards Web

- HTML, HTTP, TCP/IP
    
- GET vs POST
    
- Structure d’une requête HTTP
    
- Cycle complet d’une requête
    

## 1.3 Pages dynamiques

- JS côté client
    
- Génération côté serveur (JSP/Servlet/PHP)
    

---

# **2. Servlets**

## 2.1 Définition & rôle

- Programme Java serveur
    
- Rôle ∼ contrôleur
    

## 2.2 Cycle de vie

- Chargement
    
- init()
    
- service() → doGet()/doPost()
    
- destroy()
    

## 2.3 API Servlet

- HttpServletRequest (paramètres, cookies, headers, session)
    
- HttpServletResponse (type MIME, redirection, cookies)
    

## 2.4 Écriture d'une servlet

- Héritage HttpServlet
    
- Méthodes doGet/doPost
    
- Écriture HTML dans la réponse
    

## 2.5 Communication Servlet → JSP

- RequestDispatcher.forward
    
- sendRedirect
    
- Passage de données : request.setAttribute / session
    

---

# **3. JSP (JavaServer Pages)**

## 3.1 Rôle

- Vue dans MVC
    
- HTML dominant, Java intégré
    

## 3.2 Fonctionnement interne

- JSP → Java → .class → exécution
    

## 3.3 Objets implicites

- request, response, session, out, application…
    

## 3.4 Types de balises

- Scriptlets `<% %>`
    
- Directives `<%@ %>`
    
- Actions `<jsp:…>`
    
- Expression Language `${ }`
    

---

# **4. MVC (Web Java)**

## 4.1 Concepts

- Modèle
    
- Vue
    
- Contrôleur
    

## 4.2 Implémentation

- Servlet → Contrôleur
    
- JSP → Vue
    
- JavaBeans → Modèle
    

## 4.3 Flux MVC

- Client → Servlet → Modèle → JSP → Client
    

---

# **5. Gestion État & Utilisateurs**

## 5.1 Cookies

- Définition
    
- Stockage
    
- addCookie / getCookies
    
- Sécurité
    

## 5.2 Session (HttpSession)

- getSession()
    
- setAttribute / getAttribute
    
- Durée de vie
    
- Intérêt (panier, login…)
    

## 5.3 Paramètres URL & champs cachés

---

# **6. JDBC**

## 6.1 But

- API Java pour BD relationnelles
    

## 6.2 Étapes essentielles

1. Driver
    
2. Connexion
    
3. Statement / PreparedStatement
    
4. Exécution SQL
    
5. ResultSet
    
6. Fermeture
    

## 6.3 Transactions

- autoCommit
    
- commit / rollback
    

## 6.4 Métadonnées

- DatabaseMetaData
    
- ResultSetMetaData
    

---

# **7. Exceptions en Java**

## 7.1 Concepts

- try / catch / finally
    
- Propagation
    
- Types d’exceptions (checked / unchecked)
    

## 7.2 try-with-resources

- libération automatique
    

## 7.3 throw / throws

---

# **8. ORM, JPA & Hibernate**

## 8.1 Pourquoi un ORM ?

- Mapping objet-relationnel
    
- Gestion cache
    
- Chargement objets liés
    
- États d’un objet (éphémère / persistant / détaché)
    

## 8.2 JPA (Spécification)

- Implementations : Hibernate, EclipseLink…
    

## 8.3 Hibernate

- Mapping via annotations
    
- Session → persistance
    
- get() vs load()
    
- HQL / SQL natif / Criteria API
    

## 8.4 États d’un objet (fondamental)

- Éphémère
    
- Persistant
    
- Détaché
    
- Transitions : save / update / merge / evict
    

## 8.5 Associations

- One-to-many
    
- Many-to-many
    
- Table de jointure
    
- Classe d’association (avec attributs)
    
- Id composite (EmbeddedId)
    

## 8.6 Héritage ORM

- SINGLE_TABLE
    
- JOINED
    
- TABLE_PER_CLASS
    
- Avantages / inconvénients
    

---

# **9. DAO & Persistance**

## 9.1 Pattern DAO

- 1 classe ↔ 1 table
    
- CRUD
    
- Répartition couches : Métier / DAO / BD
    

## 9.2 Classes persistantes

- POJO
    
- Constructeur vide
    
- Getters/setters
    
- ID
    
- hashCode/equals
    

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