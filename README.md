# MedOps – API de supervision minimale (FastAPI)

## 📌 Présentation
**MedOps** est une API REST légère développée avec **FastAPI**, conçue pour illustrer un pipeline complet **DevOps / DevSecOps** incluant CI/CD, tests automatisés, audit de sécurité, conteneurisation et déploiement.
Bien que minimaliste (endpoint /health), elle constitue une base solide pour construire des services plus complexes.


## 🚀 Fonctionnalités actuelles
- **API** : FastAPI + Uvicorn
- **Endpoint** : `/health`
- **Tests** : vérification du bon fonctionnement via Pytest
- **Conteneurisation** : Docker + docker-compose
- **CI/CD** : GitHub Actions (tests, sécurité, build/push image)

Exemple de réponse JSON (GET /health) :
```json
{
  "status": "ok",
  "service": "medops",
  "version": "1.0.0"
}
```

## 🛠️ Stack Technique
- **Langage** : Python 3.10+
- **Framework** : FastAPI
- **Serveur** : Uvicorn
- **Sécurité & Qualité** : Bandit, pip-audit
- **Conteneurisation** : Docker, Docker Compose
- **CI/CD** : GitHub Actions 


## 📂 Structure du projet

```plaintext
medops/
├── .github/
│   └── workflows/
│       └── ci.yml                # Pipeline GitHub Actions (tests, audit, build Docker)
│
├── app/
│   ├── __init__.py               # Indique que 'app' est un package Python
│   ├── main.py                   # Point d'entrée principal de l'application (FastAPI)
│   └── requirements.txt          # Dépendances Python du projet
│
├── deploy/
│   ├── docker-compose.yml        # Orchestration multi-services (API, DB, etc.)
│   └── docker/
│       └── Dockerfile            # Image Docker pour l'application
│
├── tests/
│   └── test_health.py            # Test unitaire de l'endpoint /health
│
└── README.md                     # Documentation du projet
```


## 📋 Pré-requis
- Python 3.10+
- Docker & Docker Compose
- Git


## ⚡ Installation & Lancement

### 1) Cloner le projet
```bash
git clone https://github.com/ton-compte/medops.git
cd medops
```

### 2) (Option A) Lancer avec Docker Compose
```bash
docker-compose up --build
```

### 2) (Option B) Lancer en local (sans Docker)
```bash
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

## 🧪 Tests
Lancer la suite de tests :

```bash
pytest -q
```

Exemple de test (tests/test_health.py) :

```python
def test_sanity():
    assert 2 + 2 == 4
```

## 🔄 CI/CD
Ce projet inclut un pipeline GitHub Actions (`.github/workflows/ci.yml`) qui automatise :

- **Tests** : exécution de `pytest`
- **Analyse de sécurité** :
  - SAST Python avec **bandit**
  - Audit des dépendances avec **pip-audit**
- **Build & push** de l’image Docker *(si configuré)*

Le pipeline se déclenche sur chaque **push** ou **pull_request** vers la branche `main`.


## 📈 Améliorations prévues
- Authentification JWT et gestion CORS
- Logs d’audit applicatifs
- Rate limiting (ex. slowapi) et reverse proxy HTTPS (ex. Nginx/Caddy)
- Observabilité : Prometheus + Grafana
- Qualité code : SonarQube
- Déploiement infra : Ansible
