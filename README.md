<div align="center">

# 🚀 GitOps Continuous Delivery Platform for Amazon EKS

### Kubernetes Manifests, GitOps Deployments & Production Infrastructure

[![ArgoCD](https://img.shields.io/badge/ArgoCD-GitOps-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)](https://argo-cd.readthedocs.io/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.33-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Helm](https://img.shields.io/badge/Helm-Charts-0F1689?style=for-the-badge&logo=helm&logoColor=white)](https://helm.sh/)
[![HashiCorp Vault](https://img.shields.io/badge/Vault-Secrets-000000?style=for-the-badge&logo=vault&logoColor=white)](https://www.vaultproject.io/)
[![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Dashboards-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![AWS](https://img.shields.io/badge/AWS-EKS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/eks/)

**GitOps repository responsible for Kubernetes deployments, secrets management, monitoring, logging, and continuous delivery on Amazon EKS.**

</div>

---

# 📖 Overview

This repository contains the **GitOps Continuous Delivery (CD)** implementation for the Enterprise DevSecOps Platform.

Rather than deploying workloads directly from Jenkins, this repository acts as the **single source of truth** for the desired state of the Kubernetes cluster.

Whenever the CI pipeline publishes a new Docker image, it automatically updates the deployment manifest in this repository with the latest image tag. A GitHub webhook then notifies **ArgoCD**, which continuously monitors the repository, detects the change, and synchronizes the Kubernetes cluster to match the updated manifests.

In addition to application deployment, this repository also manages the deployment and configuration of platform services including:

- HashiCorp Vault
- cert-manager
- Prometheus
- Grafana
- Alertmanager
- MongoDB
- RBAC
- Namespaces
- Ingress
- TLS Certificates

---

# 🏗 GitOps Architecture

```text
                 Jenkins CI Pipeline
                        │
        Updates Kubernetes Manifest
                        │
                        ▼
              GitHub (GitOps Repository)
                        │
                 GitHub Webhook
                        │
                        ▼
                    ArgoCD
                        │
              Detect Manifest Changes
                        │
                        ▼
             Synchronize Desired State
                        │
                        ▼
                Amazon EKS Cluster
                        │
      ┌────────────────────────────────────┐
      │ ASP.NET Core Application           │
      │ MongoDB StatefulSet                │
      │ Vault                             │
      │ Prometheus                        │
      │ Grafana                           │
      │ cert-manager    
      │                    │
      └────────────────────────────────────┘
```

---

# 🚀 GitOps Deployment Workflow

```text
Docker Image Published
          │
          ▼
Jenkins Updates Image Tag
          │
          ▼
Push to GitOps Repository
          │
          ▼
GitHub Webhook
          │
          ▼
ArgoCD Detects Change
          │
          ▼
Manifest Synchronization
          │
          ▼
Deploy Application
          │
          ▼
Healthy Kubernetes Cluster
```

---

# ✨ Repository Features

- GitOps-based Kubernetes deployments
- Automatic synchronization using ArgoCD
- Declarative Kubernetes manifests
- Namespace isolation
- Secure HTTPS ingress
- Runtime secret injection using Vault
- MongoDB StatefulSet deployment
- RBAC configuration
- Monitoring and alerting stack
- Centralized logging
- Helm-based platform installations
- Production-style Kubernetes architecture

---

# ☸️ Kubernetes Resources

This repository manages the complete Kubernetes platform required to run the application.

| Resource | Purpose |
|----------|---------|
| Namespace | Workload isolation |
| Deployment | ASP.NET Core application |
| StatefulSet | MongoDB persistent database |
| Service | Internal ClusterIP communication |
| Ingress | External HTTPS access |
| RBAC | Secure Kubernetes authorization |
| ServiceAccount | Workload identity |
| ClusterRole | Cluster-level permissions |
| RoleBinding | Namespace access |
| ClusterIssuer | Let's Encrypt certificates |
| PersistentVolumeClaim | Persistent storage |
| ConfigMaps | Application configuration |

---

# 📂 Repository Structure

```text
Capstone-DotNET-Mongo-CD
│
├── Application Manifests
├── ArgoCD
├── Vault
├── Monitoring
│   ├── Prometheus
│   ├── Grafana
│   └── Alertmanager
├── MongoDB
├── RBAC
├── Ingress
├── cert-manager
└── README.md
```
