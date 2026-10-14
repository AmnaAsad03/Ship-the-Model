# Ship the Model

This repository focused on deploying machine learning models using FastAPI, building prediction APIs, authentication, and CRUD operations.

## Repository overview

The workspace contains several independent projects:

- `project 3/` — Secure customer churn prediction API with user authentication and JWT protection
- `churn_api/` — Simpler churn prediction API without auth
- `auth_project/` — Authentication service for user registration, login, and profile access
- `Practice/model-deployment-basics/` — Basic model training and inference example using the Iris dataset
- `Practice/todo_api/` — FastAPI CRUD example using an in-memory todo list

## Project structure

```text
Ship the Model/
├── README.md
├── .gitattributes
├── .DS_Store
├── project 3/
│   ├── .env
│   ├── README.md
│   ├── churn_pipeline.pkl
│   ├── users.db
│   └── app/
│       ├── __init__.py
│       ├── auth.py
│       ├── crud.py
│       ├── database.py
│       ├── dependencies.py
│       ├── logger.py
│       ├── main.py
│       ├── models.py
│       ├── predictor.py
│       ├── schemas.py
│       └── security.py
├── churn_api/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── logger.py
│   │   ├── main.py
│   │   ├── predictor.py
│   │   └── schemas.py
│   ├── churn_pipeline.pkl
│   └── requirements.txt
├── auth_project/
│   ├── .env
│   ├── app/
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   ├── crud.py
│   │   ├── database.py
│   │   ├── dependencies.py
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   └── security.py
│   ├── check_db.py
│   ├── report.md
│   ├── requirements.txt
│   └── users.db
├── Practice/
│   ├── model-deployment-basics/
│   │   ├── app/
│   │   │   └── main.py
│   │   ├── model.joblib
│   │   ├── requirements.txt
│   │   └── train_model.py
│   └── todo_api/
│       └── main.py
└── project 3/ ...
```

## Main learning themes

### 1. Secure model deployment
`project 3/` demonstrates a complete machine learning API workflow:

- user registration and login
- JWT-based authentication
- protected prediction endpoints
- batch prediction support
- database-backed users with SQLite
- Pydantic validation for request payloads
- model loading and inference using a pickled sklearn pipeline

This is the most complete example in the repo.

### 2. Plain ML API serving
`churn_api/` focuses on deploying a model as an API:

- FastAPI app setup
- model loading on startup
- `/` health check
- `/health` status endpoint
- `/predict` single-customer inference
- `/predict/batch` batch inference

### 3. Authentication backend
`auth_project/` covers the backend fundamentals of authentication:

- register users
- validate email and password input
- hash passwords safely with bcrypt
- generate JWT access tokens
- secure protected endpoints
- fetch current user profile

### 4. Model training basics
`Practice/model-deployment-basics/` shows the basics of:

- training an Iris flower classifier with scikit-learn
- serializing it with joblib
- exposing it through a FastAPI endpoint

### 5. CRUD and API patterns
`Practice/todo_api/` is a compact tutorial example showing:

- route definitions
- request/response models
- dependency injection
- CRUD operations
- status codes and validation

## Technologies used

- Python
- FastAPI
- Uvicorn
- Pydantic
- SQLite
- SQLAlchemy
- scikit-learn
- joblib
- pandas
- JWT / python-jose
- passlib with bcrypt

## Getting started

### Prerequisites

Make sure Python 3.10+ is installed and a virtual environment is available.

### Example: setup a project

```bash
cd "project 3"
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

If the project does not include a `requirements.txt`, install the needed packages manually, such as:

```bash
pip install fastapi uvicorn sqlalchemy pandas scikit-learn joblib python-multipart email-validator "passlib[bcrypt]" "python-jose[cryptography]"
```

### Environment variables

The auth and secure churn projects use a `.env` file. Example:

```env
SECRET_KEY=your_secret_key_here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

## Running the apps

### Secure churn API

```bash
cd "project 3"
uvicorn app.main:app --reload
```

Then open:

- http://127.0.0.1:8000/
- http://127.0.0.1:8000/docs

### Churn API

```bash
cd churn_api
uvicorn app.main:app --reload
```

### Authentication service

```bash
cd auth_project
uvicorn app.main:app --reload
```

### Basic model deployment example

```bash
cd "Practice/model-deployment-basics"
uvicorn app.main:app --reload
```

## Example API flow for the secure churn app

1. Register a new user
2. Log in and receive a JWT token
3. Include the token in the `Authorization` header
4. Call the protected prediction endpoints
5. Make single or batch churn predictions

## Notes

- This repo is designed for learning and experimentation rather than production deployment.
- The SQLite databases are lightweight local files used during development.
- The model files (`.pkl`, `.joblib`) are examples of serialized machine learning pipelines.

## Summary

`Ship the Model` is a compact training repository demonstrating how to move from model training to API deployment, add user authentication, and expose ML predictions via FastAPI. It combines theory and code examples to teach how to build simple but realistic AI-powered backend services.
