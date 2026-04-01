# ☸️ Scalable Kubernetes Microservices with Automated CI/CD Pipeline

This project demonstrates a high-availability production-grade environment orchestrated by **Kubernetes (K8s)**. It features a Python Flask application scaled across multiple replicas and a persistent Redis backend, fully automated with **GitHub Actions**.

## 🏗 System Architecture & Design
- **Orchestration:** Managed by **Minikube** on an **AWS m7i-flex-large** instance.
- **Flask Application:** Deployed with **2 replicas** to ensure high availability and load balancing.
- **Redis Backend:** Used as a high-performance in-memory data store for tracking visits.
- **Service Discovery:** Implemented K8s **ClusterIP** and **NodePort** services to manage internal and external communication.
- **Deployment Strategy:** Rolling updates to ensure zero downtime during application deployments.

## 🚀 Key Engineering Challenges Solved
- **Service-to-Pod Communication:** Configured K8s **Selectors** and **Labels** to establish a stable connection between the Flask app and the dynamic Redis pods.
- **Local Image Handling:** Configured the environment to use the internal Minikube Docker registry (`eval $(minikube docker-env)`) to optimize build speed and avoid unnecessary registry pulls.
- **Network Tunneling:** Successfully bridged the internal K8s cluster network with the AWS Public IP using `kubectl port-forward` and Security Group rules.

## 🤖 CI/CD Workflow (GitHub Actions)
The automated pipeline handles the entire lifecycle of the deployment:
1. **SSH Connection:** Securely connects to the AWS EC2 instance.
2. **Code Synchronization:** Pulls the latest version from the main branch.
3. **Internal Build:** Triggers a Docker build inside the Minikube environment.
4. **Automated Rollout:** Executes a `rollout restart` to update the cluster with zero service interruption.

## 🛠 Tech Stack
- **Tools:** Kubernetes (kubectl, minikube), Docker.
- **Automation:** GitHub Actions, YAML.
- **Language:** Python (Flask).
- **Cloud:** AWS (m7i-flex-large).
