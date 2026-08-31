# ✈️ AI Aircraft Maintenance Platform

An AI-powered aircraft maintenance platform that analyzes aircraft telemetry and flight-related data and provides AI-assisted maintenance recommendations.

The application consists of a **React/Vite frontend** and a **Python/FastAPI backend**. The application was containerized using **Docker**, container images were stored in **Amazon Elastic Container Registry (ECR)**, and the application was deployed on **Amazon Elastic Kubernetes Service (EKS)** using Kubernetes.

The project was first deployed manually using **AWS CLI, Docker, Amazon ECR, kubectl, and imperative Kubernetes commands**. After the manual deployment was successfully verified, Kubernetes YAML manifests and **GitHub Actions CI/CD** were implemented to make the deployment repeatable and automated.

---

# 📌 Project Overview

The platform provides a workflow for reviewing aircraft flight and maintenance information.

### Main capabilities

- Aircraft telemetry data upload
- Flight and engineering data analysis
- Aircraft condition review
- AI-assisted maintenance recommendations
- Maintenance-manual-grounded guidance
- FastAPI REST APIs
- React-based frontend
- Docker containerization
- Amazon ECR image storage
- Kubernetes deployment
- Amazon EKS hosting
- Amazon Bedrock integration
- GitHub Actions CI/CD automation

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Backend development |
| FastAPI | REST API backend |
| React | Frontend application |
| Vite | Frontend development and build tool |
| Docker | Application containerization |
| Amazon ECR | Docker container image registry |
| Amazon EKS | Managed Kubernetes platform |
| Kubernetes | Container orchestration and service management |
| Amazon Bedrock | AI capability |
| AWS IAM | AWS authentication and permissions |
| AWS CLI | AWS resource and EKS configuration |
| kubectl | Kubernetes cluster management |
| GitHub | Source code and project documentation |
| GitHub Actions | CI/CD automation |

---

# 🏗️ Application Architecture

```text
                         USER
                           |
                           v
                  +----------------+
                  | React Frontend |
                  |     Vite       |
                  +----------------+
                           |
                           | REST API
                           v
                  +----------------+
                  | FastAPI Backend|
                  |    Python      |
                  +----------------+
                           |
                           v
                  +----------------+
                  | Amazon Bedrock |
                  +----------------+
```

---

# ☁️ AWS Deployment Architecture

```text
                         Internet
                            |
                            v
                 +----------------------+
                 | Frontend LoadBalancer|
                 +----------------------+
                            |
                            v
                 +----------------------+
                 | Frontend Pod         |
                 | React + Vite         |
                 +----------------------+
                            |
                            | REST API
                            v
                 +----------------------+
                 | Backend LoadBalancer |
                 +----------------------+
                            |
                            v
                 +----------------------+
                 | Backend Pod          |
                 | FastAPI              |
                 +----------------------+
                            |
                            v
                 +----------------------+
                 | Amazon Bedrock       |
                 +----------------------+
```

---

# 🔄 Complete Project and Deployment Flow

```text
Project Development
        ↓
Frontend + Backend Setup
        ↓
Python Virtual Environment
        ↓
AWS CLI Configuration
        ↓
FastAPI Backend Development
        ↓
Run Backend Locally
        ↓
Dockerize Backend
        ↓
Test Backend Container Locally
        ↓
React/Vite Frontend Development
        ↓
Run Frontend Locally
        ↓
Dockerize Frontend
        ↓
Test Frontend Container Locally
        ↓
Create Amazon ECR Repositories
        ↓
Build Docker Images
        ↓
Push Images to Amazon ECR
        ↓
Create Amazon EKS Cluster
        ↓
Create EKS Managed Node Group
        ↓
Connect kubectl to EKS
        ↓
Deploy Backend using kubectl
        ↓
Expose Backend using LoadBalancer
        ↓
Configure AWS Credentials for Bedrock
        ↓
Verify Backend
        ↓
Deploy Frontend using kubectl
        ↓
Expose Frontend using LoadBalancer
        ↓
Configure Frontend Backend URL
        ↓
Rebuild Frontend Image
        ↓
Push Updated Frontend Image
        ↓
Restart Frontend Deployment
        ↓
Verify Pods / Deployments / Services
        ↓
Test Complete Application
        ↓
Create Kubernetes YAML Manifests
        ↓
Deploy Declaratively
        ↓
Create GitHub Actions CI/CD
        ↓
Automate Docker Build + ECR Push + EKS Deployment
```

---

# 📂 Repository Structure

```text
AI-AIRCRAFT-MAINTENANCE-APPLICATION/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   ├── Dockerfile
│   ├── pyproject.toml
│   ├── uv.lock
│   ├── .env.example
│   └── src/
│
├── frontend/
│   ├── src/
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   ├── Dockerfile
│   ├── .env.example
│   └── ...
│
├── kubernetes/
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   └── frontend-service.yaml
│
├── evidence/
│   ├── application/
│   └── deployment/
│
├── .gitignore
└── README.md
```

---

# 🐍 1. Backend Development

The backend is implemented using Python and FastAPI.

A Python virtual environment was created to isolate the project dependencies.

```bash
python -m venv .venv
```

Activate the virtual environment on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install project dependencies:

```bash
pip install -r requirements.txt
```

The backend application is started using FastAPI/Uvicorn.

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

The local FastAPI documentation can then be accessed at:

```text
http://localhost:8000/docs
```

---

# 🌐 2. Frontend Development

The frontend is implemented using React and Vite.

Navigate to the frontend directory:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

The Vite development application normally runs on:

```text
http://localhost:3000
```

The frontend communicates with the backend through the configured API base URL.

---

# 🐳 3. Docker Containerization

Docker was used to package the backend and frontend together with their runtime dependencies.

The objective of containerization is to make the application portable and consistent across environments.

---

## Backend Docker Image

Navigate to the backend directory:

```bash
cd backend
```

Build the backend image:

```bash
docker build -t maintenance-backend .
```

Check the created image:

```bash
docker images
```

Run the backend container locally:

```bash
docker run -p 8000:8000 maintenance-backend
```

The backend can then be tested through:

```text
http://localhost:8000/docs
```

---

## Frontend Docker Image

Navigate to the frontend directory:

```bash
cd frontend
```

Build the frontend image:

```bash
docker build -t maintenance-frontend .
```

Check Docker images:

```bash
docker images
```

Run the frontend container:

```bash
docker run -p 3000:3000 maintenance-frontend
```

The frontend can then be accessed locally through:

```text
http://localhost:3000
```

---

# ☁️ 4. Amazon ECR

Amazon Elastic Container Registry was used to store the Docker images before deploying them to Amazon EKS.

Two repositories were created:

```text
maintenance_backend
maintenance-frontend
```

The repositories are used for:

```text
Backend Docker Image
        ↓
Amazon ECR
        ↓
Amazon EKS

Frontend Docker Image
        ↓
Amazon ECR
        ↓
Amazon EKS
```

---

# 🔐 5. Authenticate Docker with Amazon ECR

AWS CLI was configured with the AWS account credentials.

Verify AWS CLI:

```bash
aws --version
```

Verify the configured AWS identity:

```bash
aws sts get-caller-identity
```

Configure the AWS region:

```bash
aws configure
```

The project used:

```text
Region: us-east-1
```

Authenticate Docker with Amazon ECR:

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```

---

# 📦 6. Build and Push Backend Image to ECR

Build the backend image:

```bash
docker build -t maintenance-backend .
```

Tag the image:

```bash
docker tag maintenance-backend:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance_backend:latest
```

Push the image:

```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance_backend:latest
```

---

# 📦 7. Build and Push Frontend Image to ECR

Build the frontend image:

```bash
docker build -t maintenance-frontend .
```

Tag the image:

```bash
docker tag maintenance-frontend:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance-frontend:latest
```

Push the image:

```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance-frontend:latest
```

---

# ☸️ 8. Amazon EKS Cluster

The application was deployed to an Amazon EKS cluster.

Cluster configuration used during deployment:

```text
Cluster Name: aircraft_maintenance
AWS Region: us-east-1
Kubernetes Version: 1.36
Node Group: aircraft_maintenance_node
Instance Type: t3.small
```

The EKS cluster was verified as active and the managed node was verified as ready.

---

# 🔧 9. Connect kubectl to Amazon EKS

Update the local kubeconfig:

```bash
aws eks update-kubeconfig --region us-east-1 --name aircraft_maintenance
```

Verify the current Kubernetes context:

```bash
kubectl config current-context
```

Check the EKS worker nodes:

```bash
kubectl get nodes
```

Expected result:

```text
STATUS
Ready
```

---

# 🚀 10. Manual Kubernetes Deployment

Before implementing declarative Kubernetes YAML and GitHub Actions automation, the application was deployed manually using imperative Kubernetes commands.

This helped verify that the Docker images, ECR repositories, EKS cluster, Kubernetes networking and application configuration were working correctly.

---

# 🔵 11. Deploy Backend Manually

Create the backend deployment:

```bash
kubectl create deployment maintenance-backend --image=<BACKEND_ECR_IMAGE_URI>
```

Verify the deployment:

```bash
kubectl get deployments
```

Check backend pods:

```bash
kubectl get pods
```

---

# 🌍 12. Expose Backend Using LoadBalancer

Expose the backend deployment:

```bash
kubectl expose deployment maintenance-backend --type=LoadBalancer --port=80 --target-port=8000
```

Check Kubernetes services:

```bash
kubectl get svc
```

The backend service receives an AWS Load Balancer DNS name.

The traffic flow is:

```text
Internet
   ↓
AWS Load Balancer
   ↓
Port 80
   ↓
Backend Pod
   ↓
FastAPI Port 8000
```

---

# 🔐 13. Configure AWS Credentials for Amazon Bedrock

The backend requires AWS credentials to communicate with Amazon Bedrock.

A Kubernetes Secret was created rather than storing credentials directly in the application source code.

Create the Kubernetes Secret:

```bash
kubectl create secret generic aws-credentials --from-literal=AWS_ACCESS_KEY_ID=<AWS_ACCESS_KEY_ID> --from-literal=AWS_SECRET_ACCESS_KEY=<AWS_SECRET_ACCESS_KEY> --from-literal=AWS_REGION=us-east-1
```

Verify the Secret exists:

```bash
kubectl get secrets
```

Inject the Secret into the backend deployment:

```bash
kubectl set env deployment/maintenance-backend --from=secret/aws-credentials
```

Restart the backend deployment:

```bash
kubectl rollout restart deployment maintenance-backend
```

Verify the rollout:

```bash
kubectl rollout status deployment maintenance-backend
```

---

# 🧪 14. Verify Backend

Check the backend pods:

```bash
kubectl get pods
```

Check the backend service:

```bash
kubectl get svc
```

View backend logs:

```bash
kubectl logs <BACKEND_POD_NAME>
```

The FastAPI API can be accessed using:

```text
http://<BACKEND_LOAD_BALANCER_DNS>/docs
```

The Swagger UI confirms that the FastAPI backend is reachable.

---

# 🟢 15. Deploy Frontend Manually

Create the frontend deployment:

```bash
kubectl create deployment maintenance-frontend --image=<FRONTEND_ECR_IMAGE_URI>
```

Verify:

```bash
kubectl get deployments
```

Check the frontend pods:

```bash
kubectl get pods
```

---

# 🌍 16. Expose Frontend Using LoadBalancer

Expose the frontend:

```bash
kubectl expose deployment maintenance-frontend --type=LoadBalancer --port=80 --target-port=3000
```

Check the service:

```bash
kubectl get svc
```

The frontend receives an AWS Load Balancer DNS name.

The traffic flow is:

```text
Internet
   ↓
AWS Load Balancer
   ↓
Port 80
   ↓
Frontend Pod
   ↓
Port 3000
```

---

# 🔗 17. Connect Frontend to Backend

Initially, the frontend used the local backend URL:

```text
http://localhost:8000
```

For the AWS deployment, the frontend API URL was changed to the backend Load Balancer DNS.

Example:

```text
VITE_API_BASE_URL=http://<BACKEND_LOAD_BALANCER_DNS>
```

The frontend must use the publicly reachable backend Load Balancer rather than `localhost`.

---

# ⚙️ 18. Configure Vite for AWS Load Balancer

The Vite configuration was updated to allow the application to be accessed through the AWS Load Balancer.

Example:

```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react],
  server: {
    host: "0.0.0.0",
    port: 3000,
    allowedHosts: true
  }
});
```

This configuration allows the frontend server to accept requests through the deployed environment.

---

# 🔄 19. Rebuild Frontend After Backend URL Change

Because the frontend API URL is included during the frontend build, the frontend Docker image was rebuilt after changing the backend URL.

Build:

```bash
docker build -t maintenance-frontend .
```

Tag:

```bash
docker tag maintenance-frontend:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance-frontend:latest
```

Push:

```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/maintenance-frontend:latest
```

Restart the Kubernetes frontend deployment:

```bash
kubectl rollout restart deployment maintenance-frontend
```

Verify:

```bash
kubectl rollout status deployment maintenance-frontend
```

---

# 🔍 20. Kubernetes Verification Commands

The following commands were used during deployment and troubleshooting.

### Check nodes

```bash
kubectl get nodes
```

Purpose:

```text
Verifies that the EKS worker nodes are connected and Ready.
```

### Check pods

```bash
kubectl get pods
```

Purpose:

```text
Shows whether backend and frontend pods are Running, Pending or failing.
```

### Check deployments

```bash
kubectl get deployments
```

Purpose:

```text
Shows desired replicas, available replicas and deployment status.
```

### Check services

```bash
kubectl get svc
```

Purpose:

```text
Displays Kubernetes services and their AWS Load Balancer endpoints.
```

### Check all resources

```bash
kubectl get all
```

Purpose:

```text
Provides an overview of pods, services, deployments and replicasets.
```

### View backend logs

```bash
kubectl logs <BACKEND_POD_NAME>
```

Purpose:

```text
Used to troubleshoot backend startup and runtime issues.
```

### View frontend logs

```bash
kubectl logs <FRONTEND_POD_NAME>
```

Purpose:

```text
Used to troubleshoot frontend container issues.
```

### Describe deployment

```bash
kubectl describe deployment maintenance-backend
```

Purpose:

```text
Provides detailed deployment events and configuration.
```

### Describe pod

```bash
kubectl describe pod <POD_NAME>
```

Purpose:

```text
Used to investigate pod scheduling, image, networking and container errors.
```

### Restart backend

```bash
kubectl rollout restart deployment maintenance-backend
```

Purpose:

```text
Restarts backend pods after configuration or environment changes.
```

### Restart frontend

```bash
kubectl rollout restart deployment maintenance-frontend
```

Purpose:

```text
Restarts frontend pods after a new image or configuration is deployed.
```

### Check rollout status

```bash
kubectl rollout status deployment maintenance-backend
```

```bash
kubectl rollout status deployment maintenance-frontend
```

Purpose:

```text
Confirms that the new deployment version becomes available successfully.
```

---

# 📋 21. Final Kubernetes Verification

After deployment, the following commands were used to verify the application:

```bash
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get svc
```

The expected architecture was:

```text
EKS Cluster
│
├── maintenance-backend
│   ├── Deployment
│   ├── Pod
│   └── LoadBalancer Service
│
└── maintenance-frontend
    ├── Deployment
    ├── Pod
    └── LoadBalancer Service
```

Example successful deployment state:

```text
maintenance-backend
READY: 1/1

maintenance-frontend
READY: 1/1
```

---

# 📜 22. Kubernetes YAML Deployment

After successfully validating the application using imperative Kubernetes commands, the Kubernetes configuration was converted into declarative YAML manifests.

The manifests are stored in:

```text
kubernetes/
```

Files include:

```text
kubernetes/
├── backend-deployment.yaml
├── backend-service.yaml
├── frontend-deployment.yaml
└── frontend-service.yaml
```

The purpose of YAML manifests is to define the desired Kubernetes state as code.

Instead of manually entering every Kubernetes command, the resources can be applied using:

```bash
kubectl apply -f kubernetes/
```

This makes deployment configuration:

- Repeatable
- Version controlled
- Easier to review
- Easier to reproduce
- Suitable for CI/CD automation

---

# 🤖 23. GitHub Actions CI/CD

GitHub Actions was added after the manual deployment was successfully validated.

The workflow is located at:

```text
.github/workflows/deploy.yml
```

The workflow automates the deployment process.

---

## CI/CD Flow

```text
Developer
    |
    | git push
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    ├── Checkout Repository
    |
    ├── Configure AWS Credentials
    |
    ├── Login to Amazon ECR
    |
    ├── Build Backend Docker Image
    |
    ├── Push Backend Image to ECR
    |
    ├── Build Frontend Docker Image
    |
    ├── Push Frontend Image to ECR
    |
    ├── Configure kubectl
    |
    ├── Update Kubernetes Manifests
    |
    ├── Create AWS Credentials Secret
    |
    ├── Deploy Kubernetes Resources
    |
    ├── Wait for Backend Rollout
    |
    ├── Wait for Frontend Rollout
    |
    └── Verify Kubernetes Resources
```

---

# 🔑 24. GitHub Actions Secrets and Variables

Sensitive credentials are not stored directly in the repository.

GitHub Actions uses repository secrets/variables for required AWS configuration.

Typical configuration includes:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
AWS_ACCOUNT_ID
```

Additional project-specific values may be configured as GitHub Actions variables or secrets depending on the workflow implementation.

Secrets should never be committed to GitHub.

---

# 🔒 25. Security and Secret Management

Environment files containing credentials are excluded from Git.

The repository uses `.gitignore` rules such as:

```gitignore
.env
*.env
.env.*
!.env.example
```

Virtual environments and generated files are also ignored:

```gitignore
.venv/
__pycache__/
*.pyc
node_modules/
dist/
```

The actual `.env` files containing credentials are therefore kept outside the Git repository.

Only example configuration files such as:

```text
.env.example
```

should be committed.

### Important

Never commit:

```text
.env
AWS Access Keys
AWS Secret Access Keys
API Keys
Passwords
Tokens
Private credentials
```

If a credential is accidentally committed, it should be revoked/rotated immediately.

---

# 🧪 26. Application Verification

The final deployed application was verified at multiple levels.

### Frontend

Verified that:

- React frontend loads successfully
- UI is accessible through the AWS Load Balancer
- Frontend communicates with the backend

### Backend

Verified that:

- FastAPI starts successfully
- Swagger documentation is accessible
- Backend service is reachable through the Load Balancer
- Backend pod is running successfully

### Kubernetes

Verified using:

```bash
kubectl get nodes
kubectl get pods
kubectl get deployments
kubectl get svc
```

### Docker

Verified that:

- Backend image was created
- Frontend image was created
- Containers could be run locally
- Images were pushed to Amazon ECR

### AWS

Verified that:

- EKS cluster is active
- Managed node group is active
- Worker node is Ready
- ECR repositories contain application images
- Load Balancer services are created

---

# 📸 27. Deployment Evidence

Project evidence is stored under:

```text
evidence/
```

The evidence demonstrates the work performed during development and deployment.

Examples include:

```text
evidence/
├── application/
│   ├── frontend-demo
│   └── backend-demo
│
└── deployment/
    ├── EKS cluster
    ├── EKS node
    ├── Kubernetes deployments
    ├── Kubernetes services
    ├── Amazon ECR
    └── GitHub Actions
```

The evidence section is intended to help reviewers understand the actual deployment process and verify the infrastructure used.

---

# 🎥 28. Application Demonstration

A demonstration video is included in the repository showing the deployed application.

The video demonstrates:

```text
Application Launch
        ↓
Frontend UI
        ↓
Flight Data Upload
        ↓
Backend Communication
        ↓
Data Processing
        ↓
AI-assisted Analysis
        ↓
Maintenance Recommendation
```

A separate backend demonstration can also be included to show the FastAPI API and backend functionality.

---

# 📦 29. Docker and Kubernetes Relationship

The deployment architecture follows this model:

```text
Application Source Code
        ↓
Dockerfile
        ↓
Docker Image
        ↓
Amazon ECR
        ↓
Amazon EKS
        ↓
Kubernetes Deployment
        ↓
Kubernetes Pod
        ↓
Kubernetes Service
        ↓
AWS Load Balancer
```

Docker handles **application packaging**.

Amazon ECR handles **container image storage**.

Kubernetes handles **container orchestration**.

Amazon EKS provides the **managed Kubernetes cluster**.

AWS Load Balancer provides **external application access**.

---

# 🔄 30. Manual Deployment vs Automated Deployment

The project demonstrates both imperative and declarative deployment approaches.

## Manual / Imperative Deployment

Commands were executed directly using:

```bash
kubectl create deployment
kubectl expose deployment
kubectl set env
kubectl rollout restart
kubectl get pods
kubectl get deployments
kubectl get svc
```

This approach was useful for:

- Initial deployment
- Troubleshooting
- Understanding Kubernetes resources
- Validating application connectivity

## Declarative Deployment

Kubernetes YAML manifests were then created.

```bash
kubectl apply -f kubernetes/
```

This approach provides:

- Version-controlled infrastructure
- Repeatability
- Consistent deployments
- Easier maintenance

## Automated Deployment

GitHub Actions was then used to automate:

```text
Code Push
   ↓
Docker Build
   ↓
ECR Push
   ↓
Kubernetes Deployment
   ↓
Rollout Verification
```

---

# 🧠 31. What I Implemented

This project demonstrates hands-on experience with:

- Python backend development
- FastAPI REST APIs
- React/Vite frontend development
- Environment configuration
- Docker image creation
- Docker container execution
- Amazon ECR
- AWS IAM
- AWS CLI
- Amazon EKS
- Kubernetes
- Kubernetes Deployments
- Kubernetes Services
- Kubernetes LoadBalancers
- Kubernetes Secrets
- Kubernetes rollout management
- Kubernetes YAML manifests
- GitHub Actions
- CI/CD automation
- Amazon Bedrock integration
- Cloud deployment troubleshooting
- Application verification

---

# 💼 32. Resume-Level Project Summary

### AI Aircraft Maintenance Platform | Python, FastAPI, React, Docker, AWS, Kubernetes, Amazon EKS, Amazon ECR, GitHub Actions

Built and deployed an AI-powered aircraft maintenance platform using a React/Vite frontend and FastAPI backend. Containerized application services with Docker, pushed images to Amazon ECR, deployed workloads on Amazon EKS using Kubernetes, exposed services through AWS Load Balancers, configured Kubernetes Secrets for AWS credentials, and integrated Amazon Bedrock for AI-assisted maintenance analysis. Implemented both imperative Kubernetes deployment and declarative YAML-based deployment, followed by GitHub Actions CI/CD automation for repeatable container build, ECR push, and EKS deployment.

---

# 🎯 33. Interview Discussion Points

The following topics can be discussed during an interview:

### Why Docker?

Docker packages the application and its dependencies into a consistent container image so that the application behaves consistently across environments.

### Why Amazon ECR?

ECR provides a private AWS container registry where Docker images can be stored and pulled by the EKS workloads.

### Why Amazon EKS?

EKS provides a managed Kubernetes control plane for running containerized workloads on AWS.

### Why Kubernetes Deployment?

A Deployment manages application Pods and provides controlled rollout and replacement of Pods.

### Why Kubernetes Service?

A Service provides stable networking to Pods. A LoadBalancer Service can expose the application externally.

### Why Kubernetes Secret?

Secrets allow sensitive configuration such as AWS credentials to be provided to workloads without hardcoding them into application source code.

### Why use `kubectl`?

`kubectl` is the command-line interface used to communicate with and manage Kubernetes clusters.

### Why YAML?

YAML provides declarative infrastructure configuration that can be version controlled and repeatedly applied.

### Why GitHub Actions?

GitHub Actions automates the build and deployment workflow whenever changes are pushed to the repository.

---

# 🧭 34. End-to-End Architecture Summary

```text
                         DEVELOPER
                             |
                             | git push
                             v
                    +------------------+
                    |     GitHub       |
                    +------------------+
                             |
                             v
                    +------------------+
                    | GitHub Actions   |
                    |      CI/CD       |
                    +------------------+
                             |
              +--------------+--------------+
              |                             |
              v                             v
       Docker Build                   Docker Build
       Backend Image                  Frontend Image
              |                             |
              v                             v
       +-------------+               +-------------+
       | Amazon ECR  |               | Amazon ECR  |
       +-------------+               +-------------+
              |                             |
              +--------------+--------------+
                             |
                             v
                    +------------------+
                    |    Amazon EKS    |
                    | Kubernetes       |
                    +------------------+
                       |            |
                       v            v
                 Backend Pod    Frontend Pod
                       |            |
                       v            |
                 Backend LB         |
                       |            |
                       +------REST--+
                             |
                             v
                    +------------------+
                    | Amazon Bedrock    |
                    +------------------+
```

---

# ✅ 35. Final Result

The final system demonstrates an end-to-end cloud deployment workflow:

```text
Develop
   ↓
Test Locally
   ↓
Containerize
   ↓
Push Images to ECR
   ↓
Deploy to EKS
   ↓
Expose Through LoadBalancer
   ↓
Connect Frontend + Backend
   ↓
Configure Secrets
   ↓
Verify Kubernetes Resources
   ↓
Create YAML Manifests
   ↓
Automate Using GitHub Actions
   ↓
Deploy and Verify Application
```

The repository contains the application source code, Docker configuration, Kubernetes manifests, CI/CD workflow and deployment evidence required to understand the complete implementation.
