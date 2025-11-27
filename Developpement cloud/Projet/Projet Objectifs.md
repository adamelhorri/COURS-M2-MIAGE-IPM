---
tags:
  - cloud
  - exos
---
# Projet : Mood Tracker Minimaliste — AWS Serverless

## Objectif du projet

Développer une application web minimaliste et élégante permettant à chaque utilisateur d’enregistrer son humeur quotidienne, d’y ajouter une courte note optionnelle et de visualiser son évolution sur la semaine.

Le tout est réalisé **entièrement en architecture serverless AWS**, pour garantir simplicité, scalabilité automatique et coût quasi nul.

---

## Stack technique

|Composant|Usage|Justification|
|---|---|---|
|**AWS Lambda**|Traitement métier (création et récupération d’humeurs)|Aucune gestion serveur, facturation à l’usage|
|**API Gateway**|Exposition des endpoints REST (`/mood`, `/mood/week`)|Interface REST sécurisée et scalable|
|**DynamoDB**|Stockage NoSQL des humeurs quotidiennes|Accès rapide, TTL intégré, facile à requêter par date|
|**S3**|Hébergement du frontend statique (HTML/CSS/JS)|Simple, économique, compatible CloudFront|
|**Terraform ou AWS CDK**|Infrastructure as Code (IaC)|Reproductibilité, déploiement automatisé|
|**(Optionnel)** Cognito|Authentification des utilisateurs|Facile à ajouter pour un MVP sécurisé|

---

##  Concepts principaux

- **Entrée d’humeur quotidienne unique par utilisateur**
    
- **Stockage horodaté** (clé composite : `userId`, `day`)
    
- **Visualisation hebdomadaire**
    
- **Nettoyage automatique** via **TTL** DynamoDB (par ex. 6 mois)
    
- **Interface épurée**, responsive, avec représentation graphique simple (Chart.js ou SVG)
    

---

## ⚙️ Fonctionnalités principales

|Fonction|Description|Endpoint|
|---|---|---|
|Créer / mettre à jour humeur du jour|Sauvegarde du mood + note|`POST /mood`|
|Consulter les humeurs de la semaine|Récupération par période|`GET /mood/week?start=YYYY-MM-DD&end=YYYY-MM-DD`|
|Vérifier la disponibilité API|Healthcheck|`GET /health`|
|Nettoyage automatique|Suppression auto (TTL) après X mois|via DDB TTL|

---

## 📦 Modèle de données DynamoDB

```mermaid
erDiagram
  MOODS {
    STRING userId
    STRING day
    STRING mood
    STRING note
    NUMBER createdAt
    NUMBER expiresAt
  }
%% PK = userId ; SK = day
%% TTL attribute = expiresAt

```

---

## 🧠 Architecture applicative

```mermaid
flowchart LR
  U[Utilisateur\nWeb ou Mobile] -->|HTTPS| UI[S3\nStatic Web]
  UI -->|POST /mood| API[(API Gateway)]
  UI -->|GET /mood/week| API
  API --> L1[Lambda createMood]
  API --> L2[Lambda getWeek]
  L1 --> DDB[(DynamoDB\nTable: moods)]
  L2 --> DDB
  IaC[Infrastructure as Code\nTerraform ou CDK] -->|crée| UI
  IaC -->|crée| API
  IaC -->|crée| L1
  IaC -->|crée| L2
  IaC -->|crée| DDB
```

---

## 📜 Contrats d’API

```mermaid
classDiagram
  class MoodAPI {
    <<HTTP>>
    +postMood()
    +getMoodWeek(start: string, end: string)
    +getHealth()
  }

  class PostMoodRequest {
    +userId: string
    +day: string
    +mood: string
    +note: string
  }

  class PostMoodResponse {
    +status: string
    +item: MoodItem
  }

  class GetMoodWeekResponse {
    +userId: string
    +start: string
    +end: string
    +items: MoodItem[]
  }

  class MoodItem {
    +day: string
    +mood: string
    +note: string
    +createdAt: number
    +expiresAt: number
  }

  MoodAPI --> PostMoodRequest : body
  MoodAPI --> PostMoodResponse : returns
  MoodAPI --> GetMoodWeekResponse : returns
  PostMoodResponse --> MoodItem
  GetMoodWeekResponse --> MoodItem

```

---

## 🔁 Séquences de fonctionnement

### Création ou mise à jour d’une humeur (POST /mood)

```mermaid
sequenceDiagram
  participant U as User (UI)
  participant API as API Gateway
  participant L as Lambda createMood
  participant DB as DynamoDB (moods)

  U->>API: POST /mood {userId, day, mood, note}
  API->>L: Invoke (event)
  L->>L: Validate payload (schema + enum)
  L->>DB: PutItem (PK=userId, SK=day, upsert)
  DB-->>L: OK
  L-->>API: 200 {status:"ok", item}
  API-->>U: 200 JSON
```

---

### Lecture des humeurs hebdomadaires (GET /mood/week)

```mermaid
sequenceDiagram
  participant U as User (UI)
  participant API as API Gateway
  participant L as Lambda getWeek
  participant DB as DynamoDB (moods)

  U->>API: GET /mood/week?start=YYYY-MM-DD&end=YYYY-MM-DD
  API->>L: Invoke (query params)
  L->>L: Resolve userId (header/cookie/local)
  L->>DB: Query PK=userId, SK between [start, end]
  DB-->>L: Items[]
  L-->>API: 200 {userId, start, end, items}
  API-->>U: 200 JSON
```

---

## 🪴 États d’une humeur

```mermaid
stateDiagram-v2
  [*] --> Draft : côté UI avant envoi
  Draft --> Saved : POST réussi
  Saved --> Updated : réécriture même jour
  Saved --> Expired : TTL atteint
  Updated --> Expired
  Expired --> [*]
```

---

## 🎨 Parcours utilisateur

```mermaid
flowchart LR
  A[Ouvrir l'app] --> B[Requête /mood/week]
  B --> C[Afficher la semaine]
  C --> D[Sélection humeur du jour]
  D --> E[POST /mood]
  E -->|200| F[Toast succès + refresh]
  E -->|Erreur| G[Toast erreur]
```

---

## 🧰 Prérequis techniques

- **AWS Account** (Free Tier suffit)
    
- **AWS CLI configuré**
    
- **Terraform ≥ 1.5** ou **AWS CDK (Python/TypeScript)**
    
- **Node.js ≥ 18** (pour les Lambdas)
    
- **npm / yarn** pour le front minimal
    
- **Optionnel :** Chart.js pour visualisation dans le navigateur
    

---

## 📈 Bonnes pratiques intégrées

- Validation des payloads (via `ajv` ou `pydantic`)
    
- Logs structurés JSON (`console.log` JSON ou `structlog`)
    
- Gestion du TTL DynamoDB
    
- Variables d’environnement (nom table, TTL, région)
    
- CORS activé (origines spécifiques)
    
- Observabilité via **CloudWatch Logs + Metrics**
    
- Alarme CloudWatch : erreurs Lambda > 1% sur 5 min
    

---

## 💡 Améliorations possibles (évolutions futures)

- Authentification via Cognito (userId = sub)
    
- Graphique d’évolution mood sur mois complet
    
- Export CSV ou PDF
    
- Fonction d’analyse : mood moyen, tendance
    
- PWA pour usage mobile hors ligne
    
