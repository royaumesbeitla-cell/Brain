# Plan d'Implémentation - Coffre-Fort Documentaire

## Objectif
Créer une solution complète de gestion documentaire sécurisée et conteneurisée ("Coffre-Fort Documentaire") incluant Mayan EDMS, une couche d'intelligence artificielle pour l'analyse, et une interface utilisateur personnalisée.

## Architecture
Le projet sera composé de plusieurs conteneurs Docker orchestrés par Docker Compose :

1.  **Frontend** : Interface utilisateur (React + Vite + TailwindCSS).
2.  **Backend** : API Gateway et logique métier (Python FastAPI).
3.  **AI Service** : Micro-service pour le résumé et l'extraction de mots-clés (Python FastAPI + SentenceTransformers/KeyBERT).
4.  **Mayan EDMS** : Moteur de GED (Gestion Électronique de Documents).
5.  **PostgreSQL** : Base de données pour Mayan.
6.  **Redis** : Broker de messages pour Mayan.

### Flux de Données
`Client (Frontend)` <-> `Backend (Gateway)` <-> `Mayan EDMS`
                                          <-> `AI Service`

## Changements Proposés

### Structure du Projet
```
coffre_fort_documentaire/
├── docker-compose.yml
├── .env
├── README.md
├── backend/              # Custom Backend
│   ├── Dockerfile
│   ├── main.py
│   └── requirements.txt
├── frontend/             # Custom Frontend
│   ├── Dockerfile
│   ├── package.json
│   ├── src/
│   └── ...
└── ai-service/           # AI Service
    ├── Dockerfile
    ├── main.py
    └── requirements.txt
```

### [NEW] Configuration Docker
-   **docker-compose.yml** : Définition de tous les services, réseaux et volumes.
-   **.env** : Variables d'environnement (mots de passe, clés secrètes).

### [NEW] Backend (FastAPI)
-   **Auth** : Proxy vers l'authentification Mayan ou gestion locale synchronisée.
-   **Documents** : Endpoints pour lister, uploader, voir les documents (proxy Mayan).
-   **Orchestration** : Lors de l'upload, envoi du document à Mayan, récupération du texte (OCR), envoi à l'IA, et sauvegarde des métadonnées (Résumé, Mots-clés) dans Mayan.

### [NEW] AI Service
-   API simple avec endpoints `/summarize` et `/extract_keywords`.
-   Utilisation de modèles locaux (ex: `all-MiniLM-L6-v2` ou `distilbart` pour le résumé si la machine le permet, sinon extraction simple). *Note: Pour un "résumé" de qualité en local sans gros GPU, on utilisera des techniques extractives ou un petit modèle seq2seq quantifié.*

### [NEW] Frontend (React)
-   Dashboard : Liste des documents avec recherche.
-   Upload : Interface de dépôt.
-   Viewer : Prévisualisation et affichage des métadonnées IA.
-   Admin : Gestion simple des utilisateurs.

## Plan de Vérification

### Automatisée
-   Build des images Docker : `docker-compose build`
-   Lancement : `docker-compose up -d`
-   Healthchecks définis dans docker-compose.

### Manuelle
1.  Lancer `docker-compose up`.
2.  Accéder au Frontend (http://localhost:3000).
3.  Se connecter (Admin par défaut).
4.  Uploader un PDF.
5.  Vérifier que le document apparaît.
6.  Attendre quelques secondes et vérifier que le résumé et les mots-clés (générés par l'IA) sont affichés dans les détails du document.
7.  Vérifier la recherche par mot-clé.
