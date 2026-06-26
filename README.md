# Vehicle-Insurance-Domain-Robust-pipleine_FastAPIs-
# 🚗 Vehicle Insurance Domain: Robust Production Pipeline

[![FastAPI](https://img.shields.io/badge/API-FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![AWS](https://img.shields.io/badge/Cloud-AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Docker](https://img.shields.io/badge/Container-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)

An enterprise-grade, highly automated Machine Learning operations platform designed to predict customer interest in vehicle insurance. This repository bypasses typical ad-hoc modeling scripts to establish a modular, production-ready pipeline architecture that seamlessly links automated data workflows to cloud-native serving infrastructures via RESTful APIs.

---

## 🔥 The Engineering Vision: Pipeline Over Scripts

The primary focus of this project is the **robustness and integrity of the engineering pipeline**. Rather than treating Machine Learning as a standalone notebook or a single training script, this project prioritizes a production-first architecture. 

Every stage—from raw data ingestion to cloud deployment—is modularized, decoupled, and wrapped around strict exception-handling and logging layers. This ensures that the entire lifecycle can heal, validate, scale, and retrain seamlessly without human intervention when new telemetry data lands in production.

---

## 🛠 Handled Step-by-Step: The End-to-End Modular Pipeline

### ⚡ Data Ingestion
The entry point of the pipeline programmatically queries live data from enterprise sources (such as MongoDB NoSQL clusters) and exports it into a clean, reproducible filesystem structure. It implements automated train-test splits immediately, converting external data streams into isolated local artifacts ready for validation.

### 🛡 Data Validation
A dedicated security guard for data integrity. This component tests incoming real-time records against a defined base schema configuration file. It actively performs **Schema Drift Detection**, dynamically checking column counts, validating data types, and flagging anomalous missing values to block corrupted data before it reaches the model.

### 🧪 Data Transformation & SMOTEENN Resampling
Vehicle insurance datasets are notoriously skewed toward negative classes, as most customers do not convert. To fix this severe class imbalance, the transformation pipeline integrates **SMOTEENN** (Synthetic Minority Over-sampling Technique combined with Edited Nearest Neighbors). This approach simultaneously generates clean synthetic examples for the minority class and clears out noisy borderline points. All scaler, encoder, and resampling steps are saved as distinct serialized artifacts to ensure complete consistency between training and real-time inference.

### 🧠 Model Training (Random Forest)
The pipeline utilizes an optimized **Random Forest Classifier**, a resilient architecture highly capable of handling non-linear spaces, multi-collinearity, and large categorical feature sets typical of insurance risk profiles. 

### ⚖ Model Evaluation & The Pusher Stage
Before any new model is permitted into production, it undergoes a strict comparison matrix against the currently active live model. It is only approved for deployment if it outperforms the legacy model by a predefined threshold delta ($\Delta$). Once verified, the **Model Pusher** automated module takes over, handling the safe packaging and shipping of the artifact to cloud storage without manual hand-offs.

---

## ☁ Cloud Infrastructure & API Serving Layer

The production runtime maps a fully scalable microservice architecture over **Amazon Web Services (AWS)** secured via strict **IAM (Identity and Access Management)** roles.

### ⚡ Live Prediction via FastAPI Engine
The user-facing application layer is a containerized **FastAPI** instance. It provides an ultra-low latency RESTful API layer exposing dedicated `/predict` endpoints for inference routing along with automated, self-generating Swagger documentation.

### 🗄 Storage & Registry (Amazon S3 & ECR)
* **Amazon S3** acts as the centralized, secure Artifact Repository holding versioned model binary files and serialized preprocessing transformers.
* **Amazon ECR** (Elastic Container Registry) serves as the secure vault holding the immutable, production-ready Dockerized images of the FastAPI application.

### 🚀 Compute & Security (Amazon EC2 & AWS IAM)
* **Amazon EC2** high-availability compute server instances execute the Docker containers to service global API consumers under continuous load.
* **AWS IAM** provides granular, least-privilege security access keys ensuring seamless, programmatic communication between the automated GitHub actions, the ECR container registries, and the EC2 runtime environment.

---

🎯 Project Workflow Summary

    Data Ingestion ➔ Data Validation ➔ Data Transformation
    Model Training ➔ Model Evaluation ➔ Model Deployment
    CI/CD Automation with GitHub Actions, Docker, AWS EC2, and ECR
