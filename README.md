🛠️ Dhanush DevOps Pipeline

Dhanush is a DevOps-driven project automating the build and deployment of a containerized full-stack application (React + Spring Boot) to Azure Kubernetes Service (AKS) using Jenkins, Docker, and Azure CLI.
🚀 What This Project Demonstrates
DevOps Skill	Description
CI/CD Automation	End-to-end Jenkins pipeline with multiple stages
Azure Integration	Login via Azure Service Principal; deploys to AKS
Docker & ACR	Builds and pushes Docker images to Azure Container Registry (ACR)
Kubernetes Deployment	Uses kubectl to apply manifests directly on Azure-managed Kubernetes
Credential Management	Securely manages Azure credentials via Jenkins credentials binding
📂 Pipeline Breakdown (Jenkinsfile)
✅ 1. Azure Login

    Authenticates to Azure using a service principal.

    Logs in to Azure Container Registry (keanu).

🏗️ 2. Docker Build

    Builds two images:

        frontend-h (React app)

        backend-h (Spring Boot app)

📤 3. Push to ACR

    Pushes both images to Azure Container Registry (keanu.azurecr.io).

☸️ 4. Kubernetes Deploy

    Retrieves AKS credentials.

    Applies frontend.yml and backend.yml Kubernetes manifests.

🔧 Tech Stack

    CI/CD: Jenkins

    Containers: Docker, ACR (Azure Container Registry)

    Cloud: Microsoft Azure (AKS)

    Orchestration: Kubernetes (kubectl)

    Source Control: GitHub

🧪 Prerequisites

    Jenkins server with Docker installed

    Azure Service Principal credentials configured in Jenkins (ID: azure_principle)

    Kubernetes manifests (frontend.yml, backend.yml)

    Access to Azure Container Registry (ACR) and AKS

📈 Potential Improvements

    ✅ Automated unit/integration testing stage

    🔐 Use secret management (e.g., Azure Key Vault or HashiCorp Vault)

    📊 Add monitoring/alerting using Prometheus/Grafana

    ⚙️ Shift from direct kubectl apply to GitOps (e.g., FluxCD or ArgoCD)
