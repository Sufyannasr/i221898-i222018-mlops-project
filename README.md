# MLOps Pipeline

An end-to-end **MLOps pipeline**, built using **Kubeflow**, **MLflow**, **Flask**, **Prometheus**, **Grafana**, **GitHub Actions**, and **Kubernetes**.

This project demonstrates a complete machine learning lifecycle:
- data ingestion
- validation
- feature engineering
- preprocessing
- multi-model training
- model evaluation
- best-model selection
- model versioning
- model serving
- monitoring
- alerting
- rollback readiness

---

# Project Architecture

The system is composed of the following components:

## Kubeflow Pipeline
Used for:
- dataset ingestion
- data validation
- feature engineering
- train/test split
- preprocessing
- training multiple models
- model evaluation
- best-model selection
- deployment gating

## MLflow
Used for:
- experiment tracking
- parameter logging
- metric logging
- artifact storage
- model versioning
- model registry

## Flask API
Used for:
- real-time inference serving
- confidence scoring
- class probability outputs
- SHAP explainability
- drift scoring
- online metric updates

## Prometheus
Used for:
- request metrics
- latency metrics
- model performance metrics
- drift metrics
- prediction counters
- alert rule evaluation

## Grafana
Used for:
- dashboard visualization
- live model monitoring
- operational alerts

## GitHub Actions
Used for:
- CI pipeline automation
- testing
- image building
- container publishing

## Kubernetes / Minikube
Used for:
- deployment orchestration
- service exposure
- pod management
- rollback capability

---

# Workflow Overview

## 1. Data Ingestion
The Kubeflow pipeline loads the dataset and stores it as a pipeline artifact.

## 2. Validation
The dataset is validated to ensure:
- data is not empty
- target column exists
- both target classes are present
- enough records exist for stratified splitting

## 3. Feature Engineering
Additional engineered features are created, including:
- statistical aggregates
- ratio-based features

## 4. Train/Test Split
Data is split using stratified sampling to preserve class distribution.

## 5. Preprocessing
Preprocessing includes:
- missing value imputation
- missing indicators
- categorical encoding logic
- infinite value cleanup

## 6. Multi-Model Training
The system trains multiple models:
- XGBoost Standard
- XGBoost Cost-Sensitive
- XGBoost + SMOTE
- LightGBM Cost-Sensitive
- Random Forest + Feature Selection

## 7. Evaluation
Each model is evaluated using:
- Accuracy
- Precision
- Recall
- F1 Score
- AUC-ROC
- False Positives
- False Negatives
- Business Cost

## 8. Best Model Selection
The best model is selected based on:
1. Highest recall
2. Lowest business cost
3. Highest AUC-ROC

## 9. Deployment Gate
The model is promoted only if:
- Recall exceeds threshold
- AUC exceeds threshold

## 10. Model Registry
MLflow logs:
- metrics
- hyperparameters
- artifacts
- model versions

## 11. Model Serving
The selected model is served through a Flask API endpoint:
- `/predict`
- `/metrics`
- `/model-metrics`

The API returns:
- prediction
- confidence score
- class probabilities
- SHAP explanations
- drift score
- model version

## 12. Monitoring
Prometheus continuously monitors:
- request count
- latency
- online accuracy
- precision
- recall
- F1 score
- drift score
- confusion matrix counters

## 13. Visualization & Alerts
Grafana dashboards display:
- live accuracy
- latency
- drift
- false positives
- false negatives

Alerts are triggered for:
- low accuracy
- high drift
- elevated false negatives
- elevated false positives

## 14. Rollback Readiness
Kubernetes provides:
- rollout history
- rollback support
- deployment stability

---

# Key Features

## Multi-Model Comparison
Instead of relying on a single model, the pipeline trains and evaluates multiple candidate models, selecting the best performer automatically.

## Model Explainability
SHAP explanations are generated for each prediction, allowing interpretation of feature contributions.

## Drift Monitoring
Incoming data is compared against the training baseline to detect data drift.

## Live Performance Monitoring
Online metrics are tracked in production to monitor model behavior over time.

## Model Versioning
MLflow tracks model versions and experiment history for reproducibility.

## Deployment Gating
Only models meeting defined performance thresholds are promoted.

## Observability
Prometheus and Grafana provide visibility into both API health and model health.

## Rollback Support
Kubernetes supports rolling updates and rollback if deployment issues occur.

---

# CI/CD Workflow

## Continuous Integration
GitHub Actions automates:
- dependency installation
- testing
- model training
- container build
- image publishing

## Continuous Training
Kubeflow automates:
- retraining
- evaluation
- model selection

## Deployment Gating
Deployment is triggered only if evaluation metrics exceed thresholds.

---

# Monitoring Metrics

The system tracks:

## API Metrics
- total requests
- prediction count
- request latency

## Model Metrics
- accuracy
- precision
- recall
- F1 score
- specificity
- balanced accuracy

## Drift Metrics
- feature drift score

## Operational Metrics
- false positives
- false negatives
- positive prediction rate

---

# Tech Stack

- **Kubeflow Pipelines**
- **MLflow**
- **Flask**
- **XGBoost**
- **LightGBM**
- **Random Forest**
- **Prometheus**
- **Grafana**
- **GitHub Actions**
- **Docker**
- **Kubernetes**
- **Minikube**

---

# Summary

This project implements a full **MLOps lifecycle**, including:

- automated training pipelines
- experiment tracking
- multi-model comparison
- deployment gating
- real-time inference
- explainability
- monitoring
- alerting
- rollback support

It demonstrates how machine learning systems can be built with **reproducibility, observability, and operational reliability** in mind.
