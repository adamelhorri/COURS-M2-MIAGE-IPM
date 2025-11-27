
# ✅ Mood Tracker Serverless — Plan de projet (Local + GitLab)

## 🧩 Environnement local

- [ ]  **Installer les outils** 
    
    - [ ] Node.js ≥ 18
        
    - [ ] Python ≥ 3.10
        
    - [ ]  Docker Desktop (pour LocalStack)
        
    - [ ]  AWS CLI (fake keys pour tests)
        
- [ ]  **Configurer LocalStack**
    
    - [ ]  Lancer conteneur LocalStack
        
    - [ ]  Créer profil AWS local (`aws configure` avec clés factices)
        
    - [ ]  Vérifier services (`awslocal dynamodb list- [ ]tables`, `awslocal s3 ls`)
        

 

## 📦 Dépôt & CI GitLab

- [ ]  **Initialiser le dépôt**
    
    - [ ]  `git init` + `README.md` + `LICENSE` + `.gitignore`
        
    - [ ]  Créer dépôt GitLab et `git push - [ ]u origin main`
        
- [ ]  **Configurer GitLab Runner local**
    
    - [ ]  Installer GitLab Runner
        
    - [ ]  `gitlab- [ ]runner register` (executor `shell` ou `docker`)
        
    - [ ]  Ajouter `.gitlab- [ ]ci.yml` avec `tags` du runner local
        

 

## ⚙️ Infrastructure as Code (Terraform)

- [ ]  **Squelette Terraform**
    
    - [ ]  Dossier `infra/terraform`
        
    - [ ]  Provider AWS pointant sur LocalStack
        
    - [ ]  State local
        
- [ ]  **Modules**
    
    - [ ]  `dynamodb_moods` (table + TTL)
        
    - [ ]  `lambdas` (2 Lambdas)
        
    - [ ]  `apigw_http` (routes + CORS)
        
    - [ ]  `s3_site` (bucket statique)
        
- [ ]  **Commandes Terraform**
    
    - [ ]  `terraform fmt`, `validate`, `plan`, `apply`
        
    - [ ]  Vérifier les outputs (URL API locale, bucket)
        

 

## 🗂 DynamoDB — Données

- [ ]  **Créer la table `moods`**
    
    - [ ]  PK : `userId` (STRING)
        
    - [ ]  SK : `day` (STRING, format YYYY- [ ]MM- [ ]DD)
        
    - [ ]  Champs : `mood`, `note`, `createdAt`, `expiresAt`
        
    - [ ]  Activer TTL sur `expiresAt`
        
- [ ]  **Insérer des données de test**
    
    - [ ]  Script Node/Python pour 7 jours d’un utilisateur
        
    - [ ]  Vérifier `Query` semaine avec `awslocal`
        

 

## 🧠 Lambdas (backend)

- [ ]  **createMood**
    
    - [ ]  Valider payload (`userId`, `day`, `mood`, `note`)
        
    - [ ]  Upsert item dans DynamoDB
        
    - [ ]  Ajouter `createdAt`, `expiresAt` calculé
        
    - [ ]  Logs JSON (niveau info)
        
- [ ]  **getWeek**
    
    - [ ]  Lire `start`, `end`, `userId`
        
    - [ ]  `Query` DDB (PK, SK between)
        
    - [ ]  Retourner `{userId,start,end,items[]}`
        
- [ ]  **Configuration**
    
    - [ ]  Variables env (TABLE_NAME, TTL_MONTHS)
        
    - [ ]  Validation schéma + réponse HTTP standard
        
- [ ]  **Tests**
    
    - [ ]  Tests unitaires avec mocks
        
    - [ ]  Tests intégration LocalStack
        

 

## 🌐 API Gateway

- [ ]  **Définir les routes**
    
    - [ ]  `POST /mood` → `createMood`
        
    - [ ]  `GET /mood/week` → `getWeek`
        
    - [ ]  `GET /health` → Lambda test ou mock
        
- [ ]  **Configurer CORS**
    
    - [ ]  Autoriser origin du front (`http://localhost:5173`)
        
    - [ ]  Méthodes `GET, POST`, headers `Content- [ ]Type, Authorization`
        
- [ ]  **Définir contrat OpenAPI**
    
    - [ ]  Fichier `openapi.yaml` minimal
        
    - [ ]  Validation via `swagger- [ ]cli validate`
        

 

## 🎨 Frontend S3 (statique)

- [ ]  **UI minimale**
    
    - [ ]  Page unique (form mood + note + bouton “Save”)
        
    - [ ]  Vue semaine (7 cases + mini chart SVG)
        
- [ ]  **Appels API**
    
    - [ ]  `fetch` POST/GET, gestion erreurs
        
    - [ ]  Sauvegarde `userId` en localStorage
        
- [ ]  **Exécution locale**
    
    - [ ]  Servir avec `vite` ou `http- [ ]server`
        
    - [ ]  Config `API_BASE_URL` pour LocalStack
        

 

## 🧾 Observabilité locale

- [ ]  Logs JSON structurés (`level`, `msg`, `context`)
    
- [ ]  Propagation `x- [ ]request- [ ]id` depuis front
    
- [ ]  Tests manuels via `awslocal logs tail`
    

 

## 🔒 Sécurité & contraintes gratuites

- [ ]  CORS restreint à ton front local
    
- [ ]  Validation stricte `mood` enum
    
- [ ]  `note` ≤ 280 caractères
    
- [ ]  Auth minimaliste via header `userId`
    
- [ ]  (Optionnel) Cognito plus tard (free tier)
    

 

## 🧪 Tests bout- [ ]en- [ ]bout

- [ ]  Scénario : créer mood, lire semaine, mettre à jour jour J
    
- [ ]  Scénario : TTL simulé (item expiré non retourné)
    
- [ ]  Script Node pour E2E
    
- [ ]  Intégrer E2E dans `.gitlab- [ ]ci.yml`
    

 

## 🔁 CI/CD local (gratuit)

- [ ]  **Pipeline GitLab local**
    
    - [ ]  Stages : `lint`, `test`, `e2e`
        
    - [ ]  Jobs taggés `local- [ ]runner`
        
    - [ ]  Cache `node_modules`
        
- [ ]  **Makefile**
    
    - [ ]  `make up` (LocalStack)
        
    - [ ]  `make tf- [ ]apply`
        
    - [ ]  `make test`, `make e2e`
        
    - [ ]  `make down`
        

 

## ☁️ Déploiement AWS (optionnel Free Tier)

- [ ]  Basculer `use_localstack=false` dans Terraform
    
- [ ]  Région `eu- [ ]west- [ ]3` (Paris)
    
- [ ]  Activer TTL, désactiver CloudFront
    
- [ ]  Taguer ressources (`project=mood- [ ]tracker`, `env=dev`)
    

 

## 📚 Documentation finale

- [ ]  `README.md` complet (setup, commandes, endpoints)
    
- [ ]  Diagrammes Mermaid (archi, modèle, séquences)
    
- [ ]  Section “LocalStack 100 % gratuit”
    
- [ ]  Section “Passage AWS (optionnel)”
    
- [ ]  Screenshot UI finale + logs CloudWatch simulés
    

 