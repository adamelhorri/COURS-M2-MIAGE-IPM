## Relative path : `src\main\java\dao\HibernateUtil.java`

  

```java

package dao;

  

import org.hibernate.HibernateException;

import org.hibernate.SessionFactory;

import org.hibernate.boot.registry.StandardServiceRegistryBuilder;

import org.hibernate.cfg.Configuration;

import org.hibernate.service.ServiceRegistry;

  
  

/**

 * Chargement de la configuration et création de la SessionFactory.

 * (hibernate.cfg.xml)

 */

public class HibernateUtil

{

    private static final SessionFactory SESSION_FACTORY;

  

    static

        {

        try {

            Configuration configuration = new Configuration();

            configuration.configure("hibernate.cfg.xml");

            System.out.println("Hibernate Configuration loaded");

  

            /**

             * Entité.

             */

            configuration.addAnnotatedClass(metier.Employe.class);

  

            configuration.addAnnotatedClass(metier.Demande.class);

            configuration.addAnnotatedClass(metier.Service.class);

            configuration.addAnnotatedClass(metier.Valider.class);

  
  
  

            ServiceRegistry serviceRegistry = new StandardServiceRegistryBuilder().applySettings(configuration.getProperties()).build();

            System.out.println("Hibernate serviceRegistry created");

  

            SESSION_FACTORY = configuration.buildSessionFactory(serviceRegistry);

            }

        catch (HibernateException ex)

            {

            /*----- Exception -----*/

            System.err.println("Initial SessionFactory creation failed.\n" + ex);

            throw new ExceptionInInitializerError(ex);

            }

        }

  

    public static SessionFactory getSessionFactory () { return SESSION_FACTORY; }

  

} /*----- Fin de la classe HibernateUtil -----*/

  

```

  

---

  

## Relative path : `src\main\java\dao\TestHibernate.java`

  

```java

package dao;

  

import java.sql.Date;

import java.util.Arrays;

  

import org.hibernate.Session;

import org.hibernate.Transaction;

  

import metier.Demande;

import metier.Employe;

import metier.Service;

import metier.Valider;

  

public class TestHibernate {

  

    public static void seedDatabase() {

        try (Session session = HibernateUtil.getSessionFactory().getCurrentSession()) {

  

            Transaction t = session.beginTransaction();

  

            // --- Employés ---

            Employe e1 = new Employe("Berro", "Alain");      // contient "er"

            Employe e2 = new Employe("Ravat", "Franck");

            Employe e3 = new Employe("Perrier", "Lucas");     // contient "er"

            Employe e4 = new Employe("Martin", "Claire");

  

            session.save(e1);

            session.save(e2);

            session.save(e3);

            session.save(e4);

  

            // --- Services ---

            Service s1 = new Service("Informatique");

            Service s2 = new Service("RH");

            Service s3 = new Service("Finance");

  

            session.save(s1);

            session.save(s2);

            session.save(s3);

  

            // --- Demandes (pour tester toutes les requêtes) ---

  

            // e1 → 3 demandes (pour la requête “> 2 demandes”)

            Demande d1 = new Demande(Date.valueOf("2025-01-05"), 5, Date.valueOf("2025-01-05"));

            Demande d2 = new Demande(Date.valueOf("2025-02-10"), 10, Date.valueOf("2025-02-10")); // >6 jours

            Demande d3 = new Demande(Date.valueOf("2025-03-12"), 3, Date.valueOf("2025-03-12"));

  

            d1.setEmploye(e1);

            d2.setEmploye(e1);

            d3.setEmploye(e1);

  

            session.save(d1);

            session.save(d2);

            session.save(d3);

  

            // e2 → 1 demande

            Demande d4 = new Demande(Date.valueOf("2025-04-01"), 2, Date.valueOf("2025-04-01"));

            d4.setEmploye(e2);

            session.save(d4);

  

            // e3 → 2 demandes

            Demande d5 = new Demande(Date.valueOf("2025-05-15"), 7, Date.valueOf("2025-05-15")); // >6 jours

            Demande d6 = new Demande(Date.valueOf("2025-06-01"), 1, Date.valueOf("2025-06-01"));

  

            d5.setEmploye(e3);

            d6.setEmploye(e3);

  

            session.save(d5);

            session.save(d6);

  

            // --- Relations TRAVAILLER (Employé ↔ Services) ---

            e1.setServices(Arrays.asList(s1, s2));

            e2.setServices(Arrays.asList(s2));

            e3.setServices(Arrays.asList(s1, s3));

            e4.setServices(Arrays.asList(s3));

  

            session.update(e1);

            session.update(e2);

            session.update(e3);

            session.update(e4);

  

            // --- VALIDER (tests OK/KO pour isValide) ---

            session.save(new Valider(s1, d1, "OK", Date.valueOf("2025-01-06")));

            session.save(new Valider(s2, d1, "OK", Date.valueOf("2025-01-07")));

  

            session.save(new Valider(s1, d2, "OK", Date.valueOf("2025-02-11")));

            session.save(new Valider(s2, d2, "KO", Date.valueOf("2025-02-11"))); // demande non valide

  

            session.save(new Valider(s1, d5, "OK", Date.valueOf("2025-05-16")));

            session.save(new Valider(s3, d5, "OK", Date.valueOf("2025-05-16")));

  

            t.commit();

        }

    }

    public static void testHQL() {

        try (Session session = HibernateUtil.getSessionFactory().getCurrentSession()) {

  

            Transaction t = session.beginTransaction();

  

            System.out.println("\n--- Employés avec plus de 2 demandes ---");

            session.createQuery(

                    "select e.nomE, count(d) " +

                    "from Employe e join e.demandes d " +

                    "group by e.nomE " +

                    "having count(d) > 2"

            ).list().forEach(row ->

                System.out.println(((Object[]) row)[0] + " → " + ((Object[]) row)[1] + " demandes")

            );

  

            System.out.println("\n--- Employés avec plus de X demandes (paramètre) ---");

            session.createQuery(

                    "select e.nomE, count(d) " +

                    "from Employe e join e.demandes d " +

                    "group by e.nomE " +

                    "having count(d) > :min"

            )

            .setParameter("min", 2)

            .list()

            .forEach(row ->

                System.out.println(((Object[]) row)[0] + " → " + ((Object[]) row)[1] + " demandes")

            );

  

            System.out.println("\n--- Liste des employés ---");

            session.createQuery("from Employe", Employe.class)

                   .list()

                   .forEach(System.out::println);

  

            System.out.println("\n--- Demandes de plus de 6 jours ---");

            session.createQuery("from Demande d where d.nbJours > 6", Demande.class)

                   .list()

                   .forEach(System.out::println);

  

            System.out.println("\n--- Employés dont le nom contient \"er\" ---");

            session.createQuery(

                    "select e.nomE, e.prenomE from Employe e where e.nomE like '%er%'"

            )

            .list()

            .forEach(row ->

                System.out.println(((Object[]) row)[0] + " " + ((Object[]) row)[1])

            );

  

            t.commit();

        }

    }

  
  

    public static void main(String[] args) {

        System.out.println("Test Hibernate : insertion des données...");

        seedDatabase();

  

        System.out.println("Initialisation BD...");

        seedDatabase();

  

        System.out.println("Exécution des requêtes HQL...");

        testHQL();

        System.out.println("Terminé !");

    }

}

  

```

  

---

  

## Relative path : `src\main\java\metier\Demande.java`

  

```java

package metier;

  

import java.sql.Date;

import java.util.List;

import java.util.Objects;

  

import javax.persistence.*;

  

@Entity

@Table(name="DEMANDE")

public class Demande {

  

    @Id

    @GeneratedValue(strategy = GenerationType.IDENTITY)

    @Column(name = "CodeD")

    private int codeD;

  

    private Date dateD;

    private int nbJours;

    private Date dateDebut;

  

    // Effectuer : plusieurs demandes → 1 employé

    @ManyToOne

    @JoinColumn(name="CodeE")

    private Employe employe;

  

    // Valider : 1 demande → plusieurs validations

    @OneToMany(mappedBy = "demande")

    private List<Valider> validations;

  

    public Demande() {}

    public Demande(Date d, int nj, Date dd) {

        this.dateD = d;

        this.nbJours = nj;

        this.dateDebut = dd;

    }

  

    public void setEmploye(Employe e) { this.employe = e; }

    public Employe getEmploye() { return employe; }

  

    public boolean isValide() {

        if (validations == null || validations.isEmpty()) return false;

        return validations.stream().allMatch(v -> v.getAvis().equals("OK"));

    }

  

    @Override

    public String toString() {

        return "Demande " + codeD + " par " + employe;

    }

}

  

```

  

---

  

## Relative path : `src\main\java\metier\Employe.java`

  

```java

package metier;

  

import java.util.List;

import java.util.Objects;

  

import javax.persistence.*;

  

@Entity

@Table(name="EMPLOYE")

public class Employe {

  

    @Id

    @GeneratedValue(strategy = GenerationType.IDENTITY)

    @Column(name = "CodeE")

    private int codeE;

  

    private String nomE;

    private String prenomE;

  

    // Effectuer : 1 employé → plusieurs demandes

    @OneToMany(mappedBy = "employe")

    private List<Demande> demandes;

  

    // Travailler : N employés → N services

    @ManyToMany

    @JoinTable(

        name="TRAVAILLER",

        joinColumns = @JoinColumn(name="CodeE"),

        inverseJoinColumns = @JoinColumn(name="CodeS")

    )

    private List<Service> services;

  

    public Employe() {}

    public Employe(String nom, String prenom) {

        this.nomE = nom;

        this.prenomE = prenom;

    }

  

    public int getCodeE() { return codeE; }

    public String getNomE() { return nomE; }

    public String getPrenomE() { return prenomE; }

  

    public List<Demande> getDemandes() { return demandes; }

    public void setDemandes(List<Demande> demandes) { this.demandes = demandes; }

  

    public List<Service> getServices() { return services; }

    public void setServices(List<Service> services) { this.services = services; }

  

    @Override

    public String toString() { return nomE + " " + prenomE; }

}

  

```

  

---

  

## Relative path : `src\main\java\metier\Service.java`

  

```java

package metier;

  

import java.util.List;

import java.util.Objects;

  

import javax.persistence.*;

  

@Entity

@Table(name="SERVICE")

public class Service {

  

    @Id

    @GeneratedValue(strategy = GenerationType.IDENTITY)

    @Column(name = "CodeS")

    private int codeS;

  

    private String libelleS;

  

    // Travailler : N services → N employés

    @ManyToMany(mappedBy = "services")

    private List<Employe> employes;

  

    // Valider : 1 service → plusieurs validations

    @OneToMany(mappedBy = "service")

    private List<Valider> validations;

  

    public Service() {}

    public Service(String libelle) { this.libelleS = libelle; }

  

    public int getCodeS() { return codeS; }

    public String getLibelleS() { return libelleS; }

}

  

```

  

---

  

## Relative path : `src\main\java\metier\Valider.java`

  

```java

package metier;

  

import java.sql.Date;

import javax.persistence.*;

  

@Entity

@Table(name="VALIDER")

public class Valider {

  

    @Id

    @GeneratedValue(strategy = GenerationType.IDENTITY)

    private int id;

  

    private String avis;      // "OK" ou "KO"

    private Date dateAvis;

  

    @ManyToOne

    @JoinColumn(name="CodeS")

    private Service service;

  

    @ManyToOne

    @JoinColumn(name="CodeD")

    private Demande demande;

  

    public Valider() {}

    public Valider(Service s, Demande d, String avis, Date date) {

        this.service = s;

        this.demande = d;

        this.avis = avis;

        this.dateAvis = date;

    }

  

    public String getAvis() { return avis; }

}

  

```

  

---