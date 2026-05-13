#  Note-Taking App: Complete GitOps & Observability Stack

This repository contains the declarative Kubernetes manifests for the Continuous Deployment (CD) and Infrastructure management of the Note-Taking Application. It utilizes **ArgoCD** to implement a robust GitOps pipeline on **AWS EKS**, fully integrated with an advanced observability and routing stack.

##  Project Overview
This project represents the CD and Operations portion of a complete CI/CD lifecycle. While Jenkins handles the Continuous Integration (CI) by building and pushing the Docker image, **ArgoCD** acts as the GitOps controller inside the Amazon EKS cluster. It continuously monitors this repository and automatically synchronizes the cluster state with the configurations defined here, achieving a "Single Source of Truth."

## 🏗️ Architecture & GitOps Flow
1. **CI Pipeline:** Jenkins builds the Python Flask monolithic application image and pushes it to DockerHub (`hassanmaher2001/devops-notes-app-ci`).
2. **Manifest Update:** Jenkins automatically updates the `deployment.yaml` in this repository with the newly generated image tag.
3. **CD Pipeline (ArgoCD):** Detects changes and applies them to the EKS cluster.
4. **Traffic Management:** NGINX Ingress Controller acts as the single entry point, routing external traffic efficiently and reducing cloud costs by replacing multiple AWS LoadBalancers with internal `ClusterIP` services.
5. **Observability:** A complete Prometheus and Grafana stack is continuously managed via ArgoCD Helm charts to monitor cluster health and application metrics.

##  Repository Structure
* **Application Core:**
  * `namespace.yaml`: Creates an isolated environment (`notes-app-ns`).
  * `configmap.yaml`: Injects application environment variables.
  * `deployment.yaml`: Manages High Availability with application Pod replicas.
  * `service.yaml`: Configured as `ClusterIP` to secure the app internally.
* **Routing & Ingress:**
  * `notes-ingress.yaml`: Routes public traffic via AWS LoadBalancer to the Notes app using a Catch-All rule.
  * `grafana-ingress.yaml` & `argocd-ingress.yaml`: Secures administrative tools via internal `.local` hostnames.
* **Infrastructure as Code (ArgoCD Apps):**
  * `nginx-ingress-app.yaml`: Bootstraps the NGINX Ingress Controller via Helm.
  * `prometheus-app.yaml`: Bootstraps the Kube-Prometheus-Stack for monitoring.

##  Technologies Used
* **Cloud Infrastructure:** AWS EKS (Elastic Kubernetes Service)
* **GitOps & CD:** ArgoCD
* **Containerization:** Docker
* **Traffic Routing:** NGINX Ingress Controller
* **Observability:** Prometheus & Grafana
* **Application Stack:** Python (Flask), HTML/CSS, SQLite

##  Future Enhancements (Phase 2)
* **Microservices Architecture:** Refactor the monolithic application by decoupling the Frontend and Backend to enhance scalability.
* **Stateful Storage:** Implement Persistent Volumes (PV) and Persistent Volume Claims (PVC) to retain SQLite database records across Pod restarts.
* **Public DNS Integration:** Map the Ingress LoadBalancer to a public registered domain name with valid TLS/SSL certificates.

---
**👨 Author:** Hassan Maher  
*Developed as part of the Digital Egypt Pioneers Initiative - DEPI - DevOps & Cloud Computing Track, under the supervision of Eng. Mohamed Atta.*