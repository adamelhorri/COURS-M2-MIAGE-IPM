## Relative path : `main\java\example\HelloServlet.java`

  

```java

package example;

  

import java.io.*;

import jakarta.servlet.*;

import jakarta.servlet.http.*;

import jakarta.servlet.annotation.WebServlet;

  

@WebServlet("/HelloServlet")

public class HelloServlet extends HttpServlet {

    @Override

    protected void doGet(HttpServletRequest request, HttpServletResponse response)

            throws IOException {

        response.setContentType("text/html");

        PrintWriter out = response.getWriter();

        out.println("<h1>Hello from Servlet!</h1>");

        out.println("<a href='hello.jsp'>Go to JSP</a>");

    }

}

  

```

  

---

  

## Relative path : `main\java\example\dao\CommentDao.java`

  

```java

package example.dao;

  

import example.db.DB;

import example.model.Comment;

  

import java.sql.*;

import java.util.ArrayList;

import java.util.List;

  

public class CommentDao {

  

    public void ensureTable() throws SQLException {

        String sql = """

            CREATE TABLE IF NOT EXISTS Message (

                NumMsg INT AUTO_INCREMENT PRIMARY KEY,

                Pseudo VARCHAR(50) NOT NULL,

                Texte TEXT NOT NULL

            )

        """;

        try (Connection c = DB.get(); Statement st = c.createStatement()) {

            st.execute(sql);

        }

    }

  

    public List<Comment> findAll() throws SQLException {

        String sql = "SELECT NumMsg, Pseudo, Texte FROM Message ORDER BY NumMsg DESC";

        try (Connection c = DB.get();

             PreparedStatement ps = c.prepareStatement(sql);

             ResultSet rs = ps.executeQuery()) {

  

            List<Comment> out = new ArrayList<>();

            while (rs.next()) {

                out.add(new Comment(

                        rs.getInt("NumMsg"),

                        rs.getString("Pseudo"),

                        rs.getString("Texte")

                ));

            }

            return out;

        }

    }

  

    public Comment findById(int id) throws SQLException {

        String sql = "SELECT NumMsg, Pseudo, Texte FROM Message WHERE NumMsg=?";

        try (Connection c = DB.get();

             PreparedStatement ps = c.prepareStatement(sql)) {

  

            ps.setInt(1, id);

            try (ResultSet rs = ps.executeQuery()) {

                if (rs.next()) {

                    return new Comment(

                            rs.getInt("NumMsg"),

                            rs.getString("Pseudo"),

                            rs.getString("Texte")

                    );

                }

                return null;

            }

        }

    }

  

    public void insert(Comment cm) throws SQLException {

        String sql = "INSERT INTO Message(Pseudo, Texte) VALUES(?, ?)";

        try (Connection c = DB.get();

             PreparedStatement ps = c.prepareStatement(sql)) {

  

            ps.setString(1, cm.getNom());

            ps.setString(2, cm.getMessage());

            ps.executeUpdate();

        }

    }

  

    public void update(Comment cm) throws SQLException {

        String sql = "UPDATE Message SET Pseudo=?, Texte=? WHERE NumMsg=?";

        try (Connection c = DB.get();

             PreparedStatement ps = c.prepareStatement(sql)) {

  

            ps.setString(1, cm.getNom());

            ps.setString(2, cm.getMessage());

            ps.setInt(3, cm.getId());

            ps.executeUpdate();

        }

    }

  

    public void delete(int id) throws SQLException {

        String sql = "DELETE FROM Message WHERE NumMsg=?";

        try (Connection c = DB.get();

             PreparedStatement ps = c.prepareStatement(sql)) {

  

            ps.setInt(1, id);

            ps.executeUpdate();

        }

    }

}

  

```

  

---

  

## Relative path : `main\java\example\db\DB.java`

  

```java

package example.db;

  

import java.sql.Connection;

import java.sql.DriverManager;

import java.sql.SQLException;

  

public class DB {

  

    private static final String URL =

            "jdbc:mysql://localhost:3307/app?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";

    private static final String USER = "app";

    private static final String PASS = "change_me_app";

  

    public static Connection get() throws SQLException {

        try {

            Class.forName("com.mysql.cj.jdbc.Driver");

        } catch (ClassNotFoundException e) {

            throw new SQLException("Driver MySQL introuvable.", e);

        }

        return DriverManager.getConnection(URL, USER, PASS);

    }

}

  

```

  

---

  

## Relative path : `main\java\example\model\Comment.java`

  

```java

package example.model;

  

public class Comment {

    private int id;         // NumMsg

    private String nom;     // Pseudo

    private String message; // Texte

  

    public Comment() {}

  

    public Comment(int id, String nom, String message) {

        this.id = id;

        this.nom = nom;

        this.message = message;

    }

  

    public Comment(String nom, String message) {

        this.nom = nom;

        this.message = message;

    }

  

    public int getId() { return id; }

    public void setId(int id) { this.id = id; }

  

    public String getNom() { return nom; }

    public void setNom(String nom) { this.nom = nom; }

  

    public String getMessage() { return message; }

    public void setMessage(String message) { this.message = message; }

}

  

```

  

---

  

## Relative path : `main\java\example\web\CommentServlet.java`

  

```java

package example.web;

  

import example.dao.CommentDao;

import example.model.Comment;

import jakarta.servlet.ServletException;

import jakarta.servlet.annotation.WebServlet;

import jakarta.servlet.http.*;

import jakarta.servlet.RequestDispatcher;

import java.io.IOException;

import java.sql.SQLException;

import java.util.List;

  

@WebServlet("/comments")

public class CommentServlet extends HttpServlet {

  

    private final CommentDao dao = new CommentDao();

  

    @Override

    public void init() {

        try { dao.ensureTable(); } catch (SQLException ignored) {}

    }

  

    @Override

    protected void doGet(HttpServletRequest req, HttpServletResponse resp)

            throws ServletException, IOException {

  

        req.setCharacterEncoding("UTF-8");

        String action = n(req.getParameter("action"));

  

        try {

            switch (action) {

  

                case "new" -> {

                    req.setAttribute("mode", "create");

                    forward(req, resp, "/comment_form.jsp");

                }

  

                case "edit" -> {

                    Comment c = dao.findById(Integer.parseInt(req.getParameter("id")));

                    if (c == null) { resp.sendRedirect("comments"); return; }

                    req.setAttribute("mode", "edit");

                    req.setAttribute("comment", c);

                    forward(req, resp, "/comment_form.jsp");

                }

  

                case "confirmDelete" -> {

                    String[] ids = req.getParameterValues("id");

                    if (ids == null) { resp.sendRedirect("comments"); return; }

                    req.setAttribute("ids", ids);

                    forward(req, resp, "/delete_confirm.jsp");

                }

  

                case "delete" -> {

                    String[] ids = req.getParameter("ids").split(",");

                    int count = 0;

                    for (String id : ids) {

                        dao.delete(Integer.parseInt(id));

                        count++;

                    }

                    req.setAttribute("result", count + " message(s) supprimé(s).");

                    forward(req, resp, "/delete_result.jsp");

                }

  

                default -> {

                    req.setAttribute("comments", dao.findAll());

                    forward(req, resp, "/comments.jsp");

                }

            }

  

        } catch (Exception e) {

            req.setAttribute("error", e.getMessage());

            forward(req, resp, "/comments.jsp");

        }

    }

  

    @Override

    protected void doPost(HttpServletRequest req, HttpServletResponse resp)

            throws IOException, ServletException {

  

        req.setCharacterEncoding("UTF-8");

        String action = n(req.getParameter("action"));

  

        try {

            switch (action) {

  

                case "create" -> {

                    dao.insert(new Comment(

                            req.getParameter("nom"),

                            req.getParameter("message")

                    ));

                    req.setAttribute("result", "Message ajouté avec succès.");

                    forward(req, resp, "/add_result.jsp");

                }

  

                case "update" -> {

                    Comment c = new Comment(

                            req.getParameter("nom"),

                            req.getParameter("message")

                    );

                    c.setId(Integer.parseInt(req.getParameter("id")));

                    dao.update(c);

  

                    req.setAttribute("result", "Message modifié avec succès.");

                    forward(req, resp, "/modify_result.jsp");

                }

  

                case "confirmDelete" -> doGet(req, resp);

  

                default -> resp.sendRedirect("comments");

            }

  

        } catch (Exception e) {

            req.setAttribute("error", e.getMessage());

            forward(req, resp, "/comments.jsp");

        }

    }

  

    private void forward(HttpServletRequest req, HttpServletResponse resp, String jsp)

            throws ServletException, IOException {

        req.getRequestDispatcher(jsp).forward(req, resp);

    }

  

    private String n(String s) { return s == null ? "" : s; }

}

  

```

  

---

  

## Relative path : `main\webapp\add_result.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Ajout réussi</title>

    <style>

        body { font-family: sans-serif; max-width: 600px; margin: 24px auto; }

    </style>

</head>

<body>

  

<h2>Compte-rendu</h2>

  

<p><%= request.getAttribute("result") %></p>

  

<p><a href="comments">Retour à la liste</a></p>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\comments.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Messages</title>

    <style>

        body { font-family: sans-serif; max-width: 800px; margin: 24px auto; }

        table { border-collapse: collapse; width: 100%; }

        th, td { border: 1px solid #ccc; padding: 8px; }

        .top { display:flex; justify-content:space-between; align-items:center; margin-bottom:12px; }

        .err { color:#b00; margin:8px 0; }

        button { margin-top: 10px; }

    </style>

</head>

<body>

  

<div class="top">

    <h2>Livre d’or</h2>

    <a href="comments?action=new">+ Nouveau</a>

</div>

  

<%

    String err = (String) request.getAttribute("error");

    if (err != null) {

%>

    <div class="err"><%= err %></div>

<% } %>

  

<form method="post" action="comments">

    <input type="hidden" name="action" value="confirmDelete">

  

<table>

    <tr>

        <th>Choisir</th>

        <th>ID</th>

        <th>Pseudo</th>

        <th>Message</th>

        <th>Actions</th>

    </tr>

  

<%

    java.util.List<example.model.Comment> list =

        (java.util.List<example.model.Comment>) request.getAttribute("comments");

  

    if (list != null && !list.isEmpty()) {

        for (example.model.Comment c : list) {

%>

    <tr>

        <td><input type="checkbox" name="id" value="<%= c.getId() %>"></td>

        <td><%= c.getId() %></td>

        <td><%= c.getNom() %></td>

        <td><%= c.getMessage() %></td>

        <td><a href="comments?action=edit&id=<%= c.getId() %>">Éditer</a></td>

    </tr>

<%

        }

    } else {

%>

    <tr><td colspan="5" style="text-align:center;">Aucun message</td></tr>

<% } %>

  

</table>

  

<button type="submit">Supprimer sélection</button>

  

</form>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\comment_form.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<%

    String mode = (String) request.getAttribute("mode");

    example.model.Comment c = (example.model.Comment) request.getAttribute("comment");

    boolean edit = "edit".equals(mode);

%>

<html>

<head>

    <title><%= edit ? "Modifier" : "Nouveau" %> message</title>

    <style>

        body { font-family: sans-serif; max-width: 600px; margin: 24px auto; }

        label { display:block; margin: 8px 0 4px; }

        input[type=text], textarea { width:100%; padding:8px; }

        .actions { margin-top: 12px; display:flex; gap:8px; }

    </style>

</head>

<body>

  

<h2><%= edit ? "Modifier" : "Nouveau" %> message</h2>

  

<form method="post" action="comments">

    <input type="hidden" name="action" value="<%= edit ? "update" : "create" %>">

  

    <% if (edit) { %>

        <input type="hidden" name="id" value="<%= c.getId() %>">

    <% } %>

  

    <label>Pseudo</label>

    <input type="text" name="nom" required value="<%= edit ? c.getNom() : "" %>">

  

    <label>Message</label>

    <textarea name="message" rows="5" required><%= edit ? c.getMessage() : "" %></textarea>

  

    <div class="actions">

        <button type="submit"><%= edit ? "Mettre à jour" : "Créer" %></button>

        <a href="comments">Annuler</a>

    </div>

</form>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\delete_confirm.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Confirmation suppression</title>

    <style>

        body { font-family: sans-serif; max-width:600px; margin:20px auto; }

    </style>

</head>

<body>

  

<h2>Confirmer la suppression</h2>

  

<%

    String[] ids = request.getParameterValues("id");

    if (ids == null) ids = new String[0];

%>

  

<p>Vous êtes sur le point de supprimer les messages suivants :</p>

  

<ul>

<% for (String id : ids) { %>

    <li>ID : <%= id %></li>

<% } %>

</ul>

  

<p>

    <a href="comments?action=delete&ids=<%= String.join(",", ids) %>">Oui</a> &nbsp;

    <a href="comments">Non</a>

</p>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\delete_result.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Résultat suppression</title>

    <style>

        body { font-family: sans-serif; max-width:600px; margin:20px auto; }

    </style>

</head>

<body>

  

<h2>Compte-rendu de la suppression</h2>

  

<%

    String result = (String) request.getAttribute("result");

%>

  

<p><%= result %></p>

  

<p><a href="comments">Retour à la liste</a></p>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\hello.jsp`

  

```jsp

<%@ page contentType="text/html;charset=UTF-8" %>

<html>

<head><title>Hello JSP</title></head>

<body>

<h2>Hello from JSP!</h2>

<p>This page is displayed after the Servlet.</p>

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\index.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Page d'accueil</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

  

<h2>Le livre d'or</h2>

  

<ul>

    <li><a href="comments?action=new">Saisir un message</a></li>

    <li><a href="comments">Afficher les messages</a></li>

    <li><a href="comments">Supprimer un ou plusieurs message(s)</a></li>

</ul>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\modify_result.jsp`

  

```jsp

<%@ page contentType="text/html; charset=UTF-8" %>

<html>

<head>

    <title>Modification réussie</title>

    <style>

        body { font-family: sans-serif; max-width: 600px; margin: 24px auto; }

    </style>

</head>

<body>

  

<h2>Compte-rendu de la modification</h2>

  

<p>Le message a bien été mis à jour.</p>

  

<p><a href="comments">Retour à la liste</a></p>

  

</body>

</html>

  

```

  

---

  

## Relative path : `main\webapp\WEB-INF\style.css`

  

```css

@charset "UTF-8";

  

```

  

---