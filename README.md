# 🚗 MLOps Ride Demand Prediction — Self-Healing ML System

> A production-grade MLOps system that predicts ride demand and **continuously improves itself** through automated monitoring, drift detection, retraining, and canary deployment.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115-green)
![MLflow](https://img.shields.io/badge/MLflow-2.19-orange)
![Docker](https://img.shields.io/badge/Docker-Ready-blue)

---

## 📋 Architecture

```
User → API → Model Prediction
               ↓
         Logging System
               ↓
       Monitoring (Daily Check)
               ↓
   If performance drops → Retrain
               ↓
        Model Registry (MLflow)
               ↓
     Canary Deployment → Full Release
```

## 🚀 Quick Start

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Generate Data
```bash
python data/generate_data.py
```

### 3. Train Initial Model
```bash
python src/train.py
```

### 4. Start API Server
```bash
python -m api.app
```

### 5. Open Dashboard
Navigate to `http://localhost:8000` for the monitoring dashboard.

---

## 📁 Project Structure

```
SELF_HEAL/
│
├── config.yaml                    # Central configuration
├── requirements.txt               # Dependencies
├── Dockerfile                     # Container setup
├── docker-compose.yml             # Full stack deployment
├── dvc.yaml                       # DVC pipeline definition
│
├── data/
│   ├── generate_data.py           # Synthetic data generator
│   ├── raw/                       # Raw datasets (DVC managed)
│   ├── processed/                 # Preprocessed data
│   └── logs/                      # Prediction logs
│
├── src/
│   ├── preprocess.py              # Data preprocessing & feature engineering
│   ├── train.py                   # Model training with MLflow
│   └── evaluate.py                # Model evaluation & comparison
│
├── api/
│   ├── app.py                     # FastAPI application
│   └── logger.py                  # Prediction logging system
│
├── monitoring/
│   └── monitor.py                 # Performance monitoring & drift detection
│
├── pipeline/
│   └── retrain.py                 # Automated retraining pipeline
│
├── dashboard/
│   └── index.html                 # Monitoring dashboard UI
│
├── tests/
│   └── test_system.py             # Test suite
│
└── .github/workflows/
    └── pipeline.yml               # CI/CD pipeline
```

## 🔑 Key Features

| Feature | Description |
|---------|-------------|
| **Canary Deployment** | 90/10 traffic split between champion/challenger models |
| **Drift Detection** | Statistical tests (KS, Mann-Whitney) for data/prediction drift |
| **Auto-Retraining** | Pipeline triggers when RMSE exceeds threshold |
| **MLflow Tracking** | Full experiment tracking with metrics, params, artifacts |
| **Real-time Dashboard** | Live monitoring with RMSE charts, model info, traffic split |
| **Docker Ready** | One-command deployment with Docker Compose |
| **CI/CD** | GitHub Actions for test, monitor, retrain, deploy |

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Monitoring dashboard |
| `GET` | `/health` | Health check |
| `POST` | `/predict-demand` | Get ride demand prediction |
| `POST` | `/actual-demand` | Submit actual demand |
| `GET` | `/metrics` | Current performance metrics |
| `GET` | `/model-info` | Model metadata |
| `POST` | `/reload-models` | Reload models from disk |
| `POST` | `/simulate-traffic` | Generate test traffic |
| `GET` | `/logs` | Recent prediction logs |
| `GET` | `/docs` | Swagger API documentation |

## 🐳 Docker Deployment

```bash
docker-compose up --build
```

This starts:
- **API Server** on port 8000
- **MLflow UI** on port 5000

## 🔄 Retraining Pipeline

```bash
# Auto (checks monitoring first)
python pipeline/retrain.py

# Forced retraining
python pipeline/retrain.py --force --auto-promote

# Using drift data
python pipeline/retrain.py --force --data data/raw/ride_demand_drift.csv
```

---

## 📊 Tech Stack

| Component | Technology |
|-----------|-----------|
| Model | Scikit-learn (Random Forest) |
| API | FastAPI + Uvicorn |
| Experiment Tracking | MLflow |
| Data Versioning | DVC |
| CI/CD | GitHub Actions |
| Containerization | Docker |
| Dashboard | Vanilla HTML/CSS/JS |

---

*Built as a production-grade MLOps demonstration.*
