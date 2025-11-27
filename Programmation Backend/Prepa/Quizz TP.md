---
tags:
  - back
  - exam
---


### ❓ Q1 — Dans HelloServlet, pourquoi la méthode doGet() utilise-t-elle response.getWriter() ?
- [ ] Pour lire le HTML
- [ ] Pour écrire directement du HTML dans la réponse
- [ ] Pour initialiser la session
- [ ] Pour rediriger vers une JSP

<details><summary>➡️ Réponse</summary>
Pour **écrire le HTML** renvoyé au client.
</details>

---

### ❓ Q2 — Quel est l’intérêt de `response.setContentType("text/html")` dans HelloServlet ?
- [ ] Spécifie un charset
- [ ] Indique au navigateur que la réponse est du HTML
- [ ] Active les cookies
- [ ] Initialise JDBC

<details><summary>➡️ Réponse</summary>
Indique au navigateur que le contenu est du **HTML**.
</details>

---

### ❓ Q3 — Pourquoi HelloServlet est annotée avec @WebServlet("/HelloServlet") ?
- [ ] Pour activer JDBC
- [ ] Pour déclarer l’URL qui appelle cette servlet
- [ ] Pour charger le driver MySQL
- [ ] Pour initialiser Tomcat

<details><summary>➡️ Réponse</summary>
Elle associe la **route /HelloServlet** à la servlet.
</details>

---

### ❓ Q4 — Dans CommentDao.ensureTable(), pourquoi utilise-t-on un try-with-resources ?
- [ ] Pour compresser le SQL
- [ ] Pour libérer automatiquement la connexion et le statement
- [ ] Pour ignorer les exceptions
- [ ] Pour améliorer la sécurité

<details><summary>➡️ Réponse</summary>
Pour **fermer automatiquement** Connection et Statement.
</details>

---

### ❓ Q5 — Dans CommentDao.findAll(), que fait le bloc :
```

while (rs.next()) {  
out.add(new Comment(...));  
}

```
- [ ] Il crée la table
- [ ] Il convertit chaque ligne BD en objet Comment
- [ ] Il inscrit les messages dans Tomcat
- [ ] Il supprime les lignes BD

<details><summary>➡️ Réponse</summary>
Il fait le **mapping BD → objets**.
</details>

---

### ❓ Q6 — Pourquoi `findById` retourne null si aucun message n’est trouvé ?
- [ ] Permet de distinguer “pas trouvé” d’une erreur SQL
- [ ] Nécessaire pour Hibernate
- [ ] Requis par MySQL
- [ ] Pour optimiser la mémoire

<details><summary>➡️ Réponse</summary>
null indique **message absent**.
</details>

---

### ❓ Q7 — Quel est le rôle de `ps.setInt(1, id)` dans findById ?
- [ ] Écrire une ligne en BD
- [ ] Paramétrer la requête SQL sécurisée
- [ ] Créer une nouvelle table
- [ ] Charger le driver JDBC

<details><summary>➡️ Réponse</summary>
Évite l’injection SQL → **paramètre la requête**.
</details>

---

### ❓ Q8 — Dans insert(), pourquoi ne définit-on pas l’ID du Comment ?
- [ ] L’ID vient d’un cookie
- [ ] L’ID est AUTO_INCREMENT en BD
- [ ] Cela cause une erreur
- [ ] Le JSP le met à jour

<details><summary>➡️ Réponse</summary>
Id créé automatiquement par la BD → **AUTO_INCREMENT**.
</details>

---

### ❓ Q9 — Pourquoi DB.get() charge le driver via Class.forName ?
- [ ] Pour initialiser Tomcat
- [ ] Pour enregistrer le driver JDBC dans DriverManager
- [ ] Pour optimiser la mémoire
- [ ] Pour créer la BD

<details><summary>➡️ Réponse</summary>
Pour **enregistrer le driver** MySQL.
</details>

---

### ❓ Q10 — Dans DB.get(), pourquoi une SQLException est relancée si le driver est absent ?
- [ ] Car SQLException est checked
- [ ] Pour indiquer que la BD est inutilisable
- [ ] Pour éviter try/catch dans DAO
- [ ] Pour éviter une erreur 404

<details><summary>➡️ Réponse</summary>
Sans driver → **aucune connexion possible**.
</details>

---

### ❓ Q11 — Dans CommentServlet.init(), pourquoi ignore-t-on l’exception ensureTable() ?
- [ ] Pour cacher l’erreur dans JSP
- [ ] Car si la table existe déjà, ce n’est pas grave
- [ ] Pour accélérer Tomcat
- [ ] Pour forcer une redirection

<details><summary>➡️ Réponse</summary>
La table existe déjà dans la plupart des cas.
</details>

---

### ❓ Q12 — Quel est le rôle de la méthode privée n() dans la servlet ?
- [ ] Normaliser les valeurs null
- [ ] Créer une nouvelle session
- [ ] Récupérer un cookie
- [ ] Appeler le DAO

<details><summary>➡️ Réponse</summary>
Évite NullPointerException en remplaçant **null par ""**.
</details>

---

### ❓ Q13 — Dans doGet(), pourquoi un switch-case sur action ?
- [ ] Pour router les différentes opérations CRUD
- [ ] Pour gérer CSS
- [ ] Pour compiler JSP
- [ ] Pour lire les cookies

<details><summary>➡️ Réponse</summary>
Router toutes les actions : **CRUD + formulaires**.
</details>

---

### ❓ Q14 — Dans le case "edit", pourquoi renvoyer vers comment_form.jsp ?
- [ ] Pour afficher le formulaire pré-rempli en édition
- [ ] Pour insérer un cookie
- [ ] Pour recompiler Tomcat
- [ ] Pour vider la session

<details><summary>➡️ Réponse</summary>
Affichage d’un **formulaire pré-rempli**.
</details>

---

### ❓ Q15 — Dans "delete", pourquoi transformer la liste d’ID en String join(",") ?
- [ ] Pour la stocker dans un cookie
- [ ] Pour passer plusieurs ID via un seul paramètre URL
- [ ] Pour réduire la taille HTML
- [ ] Pour encoder en Base64

<details><summary>➡️ Réponse</summary>
Transmission des IDs dans un **paramètre unique**.
</details>

---

### ❓ Q16 — Que se passe-t-il si dao.findAll() lève une SQLException dans le default de doGet ?
- [ ] L'application plante
- [ ] La servlet met l’erreur dans request et réaffiche comments.jsp
- [ ] Un cookie est créé
- [ ] Le serveur redémarre

<details><summary>➡️ Réponse</summary>
L’erreur est **affichée dans la JSP** via request.setAttribute("error").
</details>

---

### ❓ Q17 — Dans doPost("create"), pourquoi forward au lieu de redirect ?
- [ ] Pour éviter de perdre request.getAttribute("result")
- [ ] Pour changer l’URL
- [ ] Pour vider le cache
- [ ] Pour recompiler le JSP

<details><summary>➡️ Réponse</summary>
Les **attributes request** ne survivent pas après un redirect.
</details>

---

### ❓ Q18 — Quel risque dans ce code ?
```

String action = n(req.getParameter("action"));

```
- [ ] Injection CSS
- [ ] Évite un NullPointerException mais peut cacher un bug
- [ ] Supprime les cookies
- [ ] Ferme la connexion BD

<details><summary>➡️ Réponse</summary>
Remplacer null par "" peut **cacher des oublis d’action**.
</details>

---

### ❓ Q19 — Pourquoi comment_form.jsp utilise un champ caché pour "id" ?
- [ ] Pour passer l’ID en POST lors d’une mise à jour
- [ ] Pour chiffrer les données
- [ ] Pour créer des cookies
- [ ] Pour optimiser JDBC

<details><summary>➡️ Réponse</summary>
Pour **retrouver l’ID** lors d’un update.
</details>

---

### ❓ Q20 — Pourquoi comments.jsp mélange Java et HTML ?
- [ ] Parce que JSTL/EL n'est pas utilisé dans ce TP
- [ ] Parce que JSP ne supporte pas HTML
- [ ] Pour améliorer la performance
- [ ] Pour éviter les cookies

<details><summary>➡️ Réponse</summary>
Le TP est **JSP classique**, sans JSTL/EL.
</details>

---

### ❓ Q21 — Quel est l’intérêt de request.getParameterValues("id") dans confirmDelete ?
- [ ] Lire plusieurs valeurs envoyées par les checkbox
- [ ] Lire les cookies
- [ ] Lire le driver JDBC
- [ ] Lire la session

<details><summary>➡️ Réponse</summary>
Récupérer **plusieurs IDs** (cases cochées).
</details>

---

### ❓ Q22 — Pourquoi delete_confirm.jsp utilise String.join(",", ids) ?
- [ ] Pour afficher du JSON
- [ ] Pour concaténer les ID dans l’URL du lien "Oui"
- [ ] Pour les stocker dans une session
- [ ] Pour crypter les données

<details><summary>➡️ Réponse</summary>
Transmettre plusieurs IDs dans **une seule query string**.
</details>

---

### ❓ Q23 — Pourquoi utiliser PreparedStatement partout ?
- [ ] Pour écrire plus vite
- [ ] Pour éviter les injections SQL
- [ ] Pour créer automatiquement les tables
- [ ] Pour gérer HTML

<details><summary>➡️ Réponse</summary>
Prévention **injection SQL** + performances.
</details>

---

### ❓ Q24 — Que se passe-t-il si la BD est indisponible à l’appel de dao.insert() ?
- [ ] Le JSP s’exécute quand même
- [ ] Une exception est attrapée et affichée dans comments.jsp
- [ ] Le serveur redémarre
- [ ] Le formulaire disparaît

<details><summary>➡️ Réponse</summary>
L’erreur est attrapée → affichée dans **comments.jsp**.
</details>

---

### ❓ Q25 — Pourquoi CommentDao.update() utilise WHERE NumMsg=? ?
- [ ] Pour sélectionner les cookies
- [ ] Pour mettre à jour la bonne ligne BD
- [ ] Pour réinitialiser les sessions
- [ ] Pour effacer les JSP

<details><summary>➡️ Réponse</summary>
Pour mettre à jour **uniquement le message ciblé**.
</details>

---

### ❓ Q26 — À quoi sert le default dans le switch de doGet ?
- [ ] Charger la liste des commentaires
- [ ] Effacer la BD
- [ ] Charger les cookies
- [ ] Initialiser Tomcat

<details><summary>➡️ Réponse</summary>
Afficher la **liste des messages**.
</details>

---

### ❓ Q27 — Pourquoi forward(req,resp,"/comments.jsp") est appelé en cas d’erreur ?
- [ ] Pour afficher l’erreur dans la page principale
- [ ] Pour recompiler MySQL
- [ ] Pour vider la session
- [ ] Pour supprimer les objets Comment

<details><summary>➡️ Réponse</summary>
Affichage de l’erreur dans la **page principale**.
</details>

---

### ❓ Q28 — Que se passe-t-il si l’utilisateur soumet un formulaire sans champ "action" ?
- [ ] Erreur 500
- [ ] default du switch est utilisé
- [ ] Tomcat plante
- [ ] La BD est vidée

<details><summary>➡️ Réponse</summary>
action="" → **default**
</details>

---

### ❓ Q29 — Pourquoi les JSP sont dans webapp/ et pas dans WEB-INF/ ?
- [ ] Pour qu’elles soient accessibles directement
- [ ] Pour empêcher l'accès externe
- [ ] Pour activer JDBC
- [ ] Pour créer des cookies

<details><summary>➡️ Réponse</summary>
TP simplifié : **JSP accessibles via URL**.
</details>

---

### ❓ Q30 — Que se passe-t-il si l’utilisateur saisit un ID non entier dans edit ?
```

Comment c = dao.findById(Integer.parseInt(req.getParameter("id")));

```
- [ ] Le code ignore l’erreur
- [ ] NumberFormatException → catch → affiché dans comments.jsp
- [ ] La BD se vide
- [ ] Le JSP plante

<details><summary>➡️ Réponse</summary>
**NumberFormatException**, attrapée → erreur affichée.
</details>
