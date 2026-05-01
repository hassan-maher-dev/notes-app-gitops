# 🚀 Note-Taking App: GitOps CD Pipeline

This repository contains the Kubernetes manifests for the Continuous Deployment (CD) phase of the Note-Taking Application, applying GitOps principles using **ArgoCD** and **AWS EKS**.

## 📌 Project Overview
This project represents the CD portion of a complete CI/CD lifecycle. While Jenkins handles the Continuous Integration (CI) by building and pushing the Docker image to DockerHub, **ArgoCD** acts as the GitOps controller inside the Amazon EKS cluster. It continuously monitors this repository and automatically synchronizes the cluster state with the configurations defined here.

## 🏗️ Architecture (GitOps Flow)
1. **CI Pipeline (Jenkins):** Builds the Flask monolithic application image and pushes it to DockerHub (`hassanmaher2001/devops-notes-app-ci`).
2. **Manifest Update:** Jenkins updates the `deployment.yaml` in this Git repository with the newly generated image tag.
3. **CD Pipeline (ArgoCD):** Detects changes in this repository and automatically deploys the updated resources to the EKS cluster, pulling the new image.

## 📁 Repository Structure (`/k8s`)
* `namespace.yaml`: Creates the `notes-app-ns` isolated namespace for the project.
* `configmap.yaml`: Injects necessary environment variables (`FLASK_APP`, `FLASK_ENV`) into the application environment.
* `deployment.yaml`: Manages the application Pods (Configured initially for 2 Replicas to ensure High Availability) and exposes container port `5000`.
* `service.yaml`: Provisions an AWS `LoadBalancer` to expose the application to the internet, mapping external port `80` to internal port `5000`.

## 🛠️ Technologies Used
* **Cloud Infrastructure:** AWS EKS (Elastic Kubernetes Service)
* **Continuous Deployment (GitOps):** ArgoCD
* **Containerization:** Docker
* **Application Stack:** Python (Flask), HTML/CSS, SQLite

## 🚀 Future Enhancements (Phase 2)
* **Microservices Architecture:** Refactor the monolithic application by decoupling the Frontend and Backend to enhance scalability.
* **Stateful Storage:** Implement Persistent Volumes (PV) and Persistent Volume Claims (PVC) to retain SQLite database records across Pod restarts.
* **Advanced Networking:** Implement Ingress Controllers for optimized traffic routing and Service Discovery within the cluster.

---
**👨‍💻 Author:** Hassan Maher  
*Developed as part of the Digital Egypt Pioneers Initiative  DEPI - DevOps Track, under the supervision of Instructor Mohamed Atta.*