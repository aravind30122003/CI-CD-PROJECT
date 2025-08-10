<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/d714dde9-4a68-4a9d-ba7e-63d5cf27d0ac" />



# My-Webapp DevOps Project by CI-CD pipeline

This repository contains a simple Python Flask web application with a complete DevOps pipeline including:

- **GitHub** for source code management
- **Jenkins** for CI/CD automation
- **SonarQube** for code quality scanning
- **Trivy** for container image vulnerability scanning
- **Docker & Docker Hub** for containerization and image storage
- **Kubernetes & Helm** for container orchestration and deployment

---

## Project Structure

my-webapp/
│
├── app.py                        # Simple Flask app code
├── requirements.txt              # Python dependencies
├── Dockerfile                    # Docker image build instructions
├── sonar-project.properties      # SonarQube configuration
├── Jenkinsfile                   # Jenkins pipeline script
│
├── helm/                        # Helm chart for Kubernetes deployment
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── deployment.yaml
│       ├── service.yaml
│       └── _helpers.tpl
│
├── tests/                       # Optional unit tests folder
│   └── test_app.py              # Sample unit test
│
└── README.md                    # This file

---

## Prerequisites

- Docker installed
- Kubernetes cluster running (Minikube, Kind, or cloud)
- Helm installed
- Jenkins server configured with:
  - Docker installed
  - SonarQube plugin configured
  - Docker Hub credentials added (`dockerhub-cred`)
- SonarQube server accessible
- Trivy installed on Jenkins or Jenkins agent
- Docker Hub account

---

## Getting Started

### 1. Clone this repository

```bash
git clone https://github.com/aravind30122003/CI-CD-PROJECT.git
cd cI-CD-project

3. Configure Jenkins Pipeline
	•	Create a new pipeline job in Jenkins.
	•	Connect your GitHub repo.
	•	Add Docker Hub credentials in Jenkins (dockerhub-cred).
	•	Configure SonarQube server and add SonarQube plugin.
	•	Use the provided Jenkinsfile from the repo.
	•	Run the pipeline.


    4. Kubernetes Deployment with Helm

Ensure your Kubernetes cluster is running:
minikube start

Deploy the app using Helm via Jenkins pipeline or manually:
helm upgrade --install my-app ./helm --set image.repository=aravind30122003/CI-CD-project --set image.tag=latest

Check pods and service:

kubectl get pods
kubectl get svc



Access your app (port-forward):

kubectl port-forward svc/my-webapp 5000:5000

Open http://localhost:5000 in your browser.
