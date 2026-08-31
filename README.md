# ✈️ AI Aircraft Maintenance Platform

An AI-powered aircraft maintenance platform that analyzes aircraft telemetry data and provides maintenance recommendations.

The application consists of a React frontend and FastAPI backend. It is containerized using Docker and deployed on Amazon EKS, with container images stored in Amazon ECR.

## 🚀 Project Overview

The platform allows users to:

- Upload aircraft telemetry data in Excel format
- Generate engineering analytics
- Analyze aircraft health and operational signals
- Generate AI-powered maintenance recommendations
- Use maintenance-manual information to support maintenance guidance

## 🛠️ Technology Stack

- React
- Vite
- Python
- FastAPI
- Docker
- Amazon ECR
- Amazon EKS
- Kubernetes
- Amazon Bedrock

  ## 🏗️ Architecture

```text
                    User
                     │
                     ▼
             React Frontend
                (Vite)
                     │
                     │ REST API
                     ▼
             FastAPI Backend
                     │
                     ▼
              Amazon Bedrock
                     │
                     ▼
          AI Maintenance Recommendation


Deployment Architecture

User
 │
 ▼
Frontend Load Balancer
 │
 ▼
Frontend Pod
 │
 ├──────── REST API ────────► Backend Load Balancer
 │                                  │
 │                                  ▼
 │                            Backend Pod
 │                                  │
 │                                  ▼
 │                           Amazon Bedrock
 │
 └──────────────────────────────────────
- AWS IAM
- GitHub Actions
