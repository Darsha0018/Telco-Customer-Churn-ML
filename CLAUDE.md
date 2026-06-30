# CLAUDE.md

This document provides guidance for AI coding assistants (Claude Code) when working with the **Customer Churn Prediction System**.

---

# Project Overview

This repository implements a **production-ready end-to-end Machine Learning pipeline** for predicting customer churn in the telecom industry.

The project covers the complete ML lifecycle:

- Data Loading
- Data Validation (Great Expectations)
- Data Preprocessing
- Feature Engineering
- XGBoost Model Training
- MLflow Experiment Tracking
- FastAPI REST API
- Gradio Web Interface
- Docker Deployment
- AWS ECS Compatibility

---

# Project Structure

```
Customer-Churn-ML
│
├── data/
│   ├── raw/
│   └── processed/
│
├── scripts/
│   ├── run_pipeline.py
│   ├── prepare_processed_data.py
│   ├── test_fastapi.py
│   ├── test_pipeline_phase1_data_features.py
│   └── test_pipeline_phase2_modeling.py
│
├── src/
│   ├── app/
│   ├── data/
│   ├── features/
│   ├── models/
│   ├── serving/
│   └── utils/
│
├── mlruns/
│
├── dockerfile
├── requirements.txt
└── README.md
```

---

# Development Commands

## Create Virtual Environment

```bash
python -m venv .venv
```

Activate

Windows

```bash
.venv\Scripts\activate
```

Linux/macOS

```bash
source .venv/bin/activate
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Training Pipeline

Run the complete pipeline

```bash
python scripts/run_pipeline.py \
--input data/raw/Telco-Customer-Churn.csv \
--target Churn
```

Prepare processed dataset

```bash
python scripts/prepare_processed_data.py
```

---

# Testing

Pipeline

```bash
python scripts/test_pipeline_phase1_data_features.py
```

Model

```bash
python scripts/test_pipeline_phase2_modeling.py
```

FastAPI

```bash
python scripts/test_fastapi.py
```

---

# Running the Application

Run FastAPI

```bash
python -m uvicorn src.app.main:app --reload --host 0.0.0.0 --port 8000
```

Application

```
http://localhost:8000
```

Gradio Interface

```
http://localhost:8000/ui
```

Swagger Documentation

```
http://localhost:8000/docs
```

---

# Docker

Build

```bash
docker build -t telco-churn-app .
```

Run

```bash
docker run -p 8000:8000 telco-churn-app
```

---

# Machine Learning Workflow

```
Raw Dataset
      │
      ▼
Load Data
      │
      ▼
Validate Data
      │
      ▼
Preprocess
      │
      ▼
Feature Engineering
      │
      ▼
Train/Test Split
      │
      ▼
XGBoost Model
      │
      ▼
Evaluation
      │
      ▼
MLflow Logging
      │
      ▼
Save Model
      │
      ▼
FastAPI
      │
      ▼
Gradio UI
```

---

# Model Configuration

Algorithm

- XGBoost Classifier

Training includes

- Class Imbalance Handling
- Hyperparameter Configuration
- Feature Engineering
- Model Serialization

---

# MLflow

Tracking URI

```
./mlruns
```

Tracked Metrics

- Precision
- Recall
- F1 Score
- ROC-AUC
- Training Time
- Prediction Time
- Data Validation Status

Artifacts

- Model
- Feature Columns
- Preprocessing Metadata

---

# Feature Engineering

Binary Encoding

- Gender
- Partner
- Dependents
- PhoneService
- PaperlessBilling

One-Hot Encoding

- InternetService
- Contract
- PaymentMethod
- MultipleLines
- OnlineSecurity
- OnlineBackup
- DeviceProtection
- TechSupport
- StreamingTV
- StreamingMovies

The serving pipeline **must always use the same feature ordering and transformations as training**.

---

# API Endpoints

## GET /

Health Check

Response

```json
{
  "status": "ok"
}
```

---

## POST /predict

Predict customer churn.

Input

Customer information following the `CustomerData` schema.

Output

```
Likely to churn
```

or

```
Not likely to churn
```

---

## GET /ui

Interactive Gradio Interface

---

# Deployment

Current deployment supports

- Docker
- FastAPI
- Gradio
- MLflow
- AWS ECS
- Application Load Balancer

---

# Best Practices

- Keep training and serving feature transformations identical.
- Store every trained model in MLflow.
- Never change feature ordering after training.
- Validate datasets before model training.
- Update feature artifacts whenever retraining.

---

# Future Improvements

- SHAP Explainability
- CI/CD Enhancements
- Kubernetes Deployment
- Model Monitoring
- Drift Detection
- Automated Hyperparameter Tuning
- Cloud Model Registry

---

# Author

**Darshan Chavan**

Artificial Intelligence & Data Science Engineer

Machine Learning | MLOps | FastAPI | XGBoost | MLflow
