---
tags:
  - cloud
  - exos
---
Voici **3 diagrammes Mermaid** d’architecture détaillée (valides).

# Archi fonctionnelle (flux)

```mermaid
flowchart TB
  U[Utilisateur\nNavigateur] -->|HTTPS| UI[S3\nFrontend statique]

  subgraph API_Gateway[API Gateway HTTP]
    R1[POST mood]
    R2[GET mood_week]
    R3[GET health]
  end

  UI --> R1
  UI --> R2
  UI -.-> R3

  R1 --> L1[Lambda createMood]
  R2 --> L2[Lambda getWeek]
  R3 --> L3[Lambda healthCheck]

  subgraph Database[DynamoDB]
    T[(Table moods)]
  end
  L1 --> T
  L2 --> T

  subgraph Storage[S3]
    B[(Bucket site web)]
  end
  UI --- B

  subgraph Observabilite[CloudWatch]
    CW[(Logs & Metrics)]
  end
  L1 -. logs .-> CW
  L2 -. logs .-> CW
  L3 -. logs .-> CW
  API_Gateway -. métriques .-> CW

  subgraph IaC[Infrastructure as Code]
    TF[Terraform ou CDK]
  end
  TF -- crée --> API_Gateway
  TF -- crée --> L1
  TF -- crée --> L2
  TF -- crée --> L3
  TF -- crée --> T
  TF -- crée --> B

```

# Archi déploiement (local vs AWS)

```mermaid
flowchart LR
  Dev[Développeur local] --> Code[Repository GitLab]
  Code --> Runner[GitLab Runner\nexecutor local]
  Runner --> Build[Étape Build et Tests]
  Build -->|terraform apply local| LS[LocalStack\nDDB, S3, API, Lambda]
  Build -->|npm run dev| UIlocal[Frontend local]

  subgraph Local
    UIlocal --> APILocal[API locale 4566]
    APILocal --> LLocal[Lambda locale]
    LLocal --> DDBLocal[DynamoDB LocalStack]
    UIlocal -. fetch .-> S3Local[S3 LocalStack]
  end

  subgraph AWS[Option déploiement AWS Free Tier]
    TF[Terraform production] --> AWSAPI[API Gateway]
    TF --> AWSL1[Lambda createMood]
    TF --> AWSL2[Lambda getWeek]
    TF --> AWSLh[Lambda healthCheck]
    TF --> AWSDDB[DynamoDB moods]
    TF --> AWSS3[S3 site statique]
    Browser[Utilisateur final] --> AWSS3
    Browser --> AWSAPI
    AWSAPI --> AWSL1
    AWSAPI --> AWSL2
    AWSAPI --> AWSLh
    AWSL1 --> AWSDDB
    AWSL2 --> AWSDDB
  end

```

# Archi logique (composants et dépendances)

```mermaid
classDiagram
  class Frontend {
    +Form mood+note
    +Vue semaine
    +Fetch API
    +LocalStorage userId
  }

  class ApiGateway {
    +POST /mood
    +GET /mood/week
    +GET /health
  }

  class CreateMoodLambda {
    +validatePayload()
    +putItem()
    +computeTTL()
    +log()
  }

  class GetWeekLambda {
    +parseRange()
    +queryByUserAndDay()
    +log()
  }

  class HealthLambda {
    +ping()
  }

  class DynamoDB_Moods {
    +PK: userId (STRING)
    +SK: day (STRING YYYY-MM-DD)
    +mood, note
    +createdAt, expiresAt
  }

  class S3_Site {
    +index.html
    +assets
  }

  class IaC {
    +Terraform/CDK
    +Outputs
    +Tags
  }

  class Observabilite {
    +CloudWatch Logs
    +Metrics/Alarms
  }

  Frontend --> ApiGateway
  ApiGateway --> CreateMoodLambda
  ApiGateway --> GetWeekLambda
  ApiGateway --> HealthLambda
  CreateMoodLambda --> DynamoDB_Moods
  GetWeekLambda --> DynamoDB_Moods
  Frontend --> S3_Site
  IaC ..> ApiGateway
  IaC ..> CreateMoodLambda
  IaC ..> GetWeekLambda
  IaC ..> HealthLambda
  IaC ..> DynamoDB_Moods
  IaC ..> S3_Site
  CreateMoodLambda ..> Observabilite
  GetWeekLambda ..> Observabilite
  HealthLambda ..> Observabilite
  ApiGateway ..> Observabilite
```
