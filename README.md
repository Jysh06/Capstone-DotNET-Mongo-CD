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
---

# 🔐 Secrets Management with HashiCorp Vault

Application secrets are managed using **HashiCorp Vault**, eliminating the need to store sensitive information in Kubernetes manifests, ConfigMaps, or source code.

A highly available Vault cluster is deployed on Amazon EKS using **Helm** with custom values. The **Vault Agent Injector** automatically injects secrets into application pods at runtime through a sidecar container.

### Secret Injection Workflow

```text
Application Pod
      │
      ▼
Vault Agent Sidecar
      │
Authenticate using Kubernetes Auth
      │
      ▼
HashiCorp Vault
      │
Retrieve Secrets
      │
      ▼
Write Secrets to Shared Volume
      │
      ▼
Application Reads Secrets
```

### Highlights

- High Availability Vault deployment
- Vault Agent Injector
- Kubernetes Authentication
- Runtime secret injection
- No hardcoded credentials
- Helm-based deployment with custom values
- Centralized secret management

---

# 📊 Monitoring & Observability

The platform includes a complete monitoring stack to provide real-time visibility into the Kubernetes cluster and deployed workloads.

## Monitoring Stack

| Component | Purpose |
|----------|---------|
| Prometheus | Metrics collection |
| Node Exporter | Node-level metrics |
| Grafana | Dashboards & visualization |
| Alertmanager | Alert routing and notifications |

### Metrics Collected

- Kubernetes Cluster Health
- Node CPU & Memory Usage
- Pod Resource Utilization
- Application Performance
- Persistent Volume Usage
- Network Statistics

---

# 🔒 Platform Security

Security is integrated throughout the Kubernetes platform following DevSecOps best practices.

### Security Features

- HashiCorp Vault for secrets management
- Runtime secret injection
- Kubernetes RBAC
- Namespace isolation
- ClusterIP services for internal communication
- MongoDB inaccessible from the public internet
- HTTPS Ingress using cert-manager
- TLS certificates from Let's Encrypt
- Principle of Least Privilege
- GitOps-based deployment approvals

---

# 🏗 Namespace Architecture

The platform separates workloads into dedicated namespaces for better organization and security.

| Namespace | Purpose |
|----------|---------|
| `webapps` | ASP.NET Core application & MongoDB |
| `vault` | HashiCorp Vault |
| `monitoring` | Prometheus, Grafana & Alertmanager |
| `sonarqube` | SonarQube Server |

Namespace isolation improves security, access control, and operational management.

---

# 🌐 Application Exposure

The application is securely exposed using an **NGINX Ingress Controller**.

### Features

- HTTPS-only access
- TLS termination
- Automatic certificate management
- Let's Encrypt integration
- ClusterIP backend services
- External Load Balancer

```text
Internet
    │
    ▼
AWS Load Balancer
    │
    ▼
NGINX Ingress Controller
    │
    ▼
ClusterIP Service
    │
    ▼
ASP.NET Core Pods
```

---


# 🚀 Future Enhancements

- Argo Rollouts for Blue-Green and Canary deployments
- Horizontal Pod Autoscaler (HPA)
- Vertical Pod Autoscaler (VPA)
- Kubernetes Network Policies
- Kyverno or OPA Gatekeeper for policy enforcement
- External Secrets Operator integration
- Multi-environment GitOps (Dev, QA, Production)
- Disaster Recovery and backup automation
- Multi-cluster ArgoCD deployment

---

# 👨‍💻 Author

**Jayesh Patil**

**DevOps/DevSecOps | Cloud Engineer | Kubernetes | AWS**

- **GitHub:** https://github.com/Jysh06
- **LinkedIn:** https://www.linkedin.com/in/jayeshpatil12

---

## ⭐ If you found this project helpful, consider giving it a star!

This repository demonstrates a production-inspired **GitOps Continuous Delivery Platform** built on **Amazon EKS**, showcasing secure Kubernetes deployments, automated synchronization with ArgoCD, centralized secrets management using HashiCorp Vault, and a complete observability stack with Prometheus, Grafana, and ELK.
