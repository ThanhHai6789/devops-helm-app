GitOps Continuous Delivery Pipeline with K3s, Helm & ArgoCD

A production-ready **GitOps deployment pipeline** hosted on **AWS EC2**, leveraging **K3s**, **Helm v3**, and **ArgoCD** to automate application lifecycle management.

---

## 📌 Architecture & Stack

* **Cloud Infrastructure:** AWS EC2 (`t3.small` / Ubuntu 26.04)
* **Kubernetes Cluster:** K3s (Lightweight Kubernetes)
* **Package Manager:** Helm v3
* **GitOps Operator:** ArgoCD v3.5
* **Source Control:** GitHub

---

## 🏗️ Pipeline Overview

```text
[ Developer / Git Commit ] 
          │
          ▼ (git push)
[ GitHub Repository ]
          │
          ▼ (Auto-Polling / Sync)
[ ArgoCD Operator ] (Runs inside K3s Cluster)
          │
          ▼ (Declarative Deployment)
[ K3s Cluster ] ──► Deployments & Pods (Nginx Web App)
📁 Repository Structure
Plaintext
.
├── Chart.yaml          # Helm chart metadata
├── values.yaml         # Configuration values (Replicas, Image tags, Services)
├── templates/          # Kubernetes resource templates (Deployment, Service, HPA)
├── Dockerfile          # Application container definition
└── index.html          # Web application source
🔥 Key Highlights & Features
Declarative GitOps Management: Infrastructure and application state are fully represented as code in this repository.

Automated Reconciliation: ArgoCD automatically detects changes in GitHub and synchronizes the K3s cluster without manual SSH/kubectl intervention.

Zero-Touch Scaling Demo: Tested scaling application replicas from 1 to 2 seamlessly via git commit on values.yaml.

Self-Healing: ArgoCD automatically corrects any manual configuration drift on the cluster back to the state declared in Git.

🛠️ How to Deploy via ArgoCD
Install ArgoCD on your K3s cluster.

Create an ArgoCD Application using the following configurations:

Application Name: my-web-app

Repository URL: https://github.com/ThanhHai6789/devops-helm-app.git

Path: .

Cluster URL: https://kubernetes.default.svc

Namespace: default

Sync Policy: Automatic (Enable Prune and Self-Heal)
