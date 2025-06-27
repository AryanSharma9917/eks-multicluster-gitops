# eks-multicluster-gitops

> GitOps-driven multi-cluster application and infrastructure deployment using ArgoCD on Amazon EKS

---

## Overview

This project demonstrates a fully GitOps-managed, multi-cluster Kubernetes deployment model using [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) and [Amazon EKS](https://aws.amazon.com/eks/). It follows a **hub-and-spoke architecture**, where a central ArgoCD instance (hub) manages application and addon deployments across multiple workload clusters (spokes).

---

##  Objectives

- Provision 3 Amazon EKS clusters: `hub`, `staging`, and `prod`
- Install ArgoCD on the hub cluster
- Use GitOps to:
  - Deploy Namespaces & Platform Services
  - Deploy Applications (backend, frontend)
  - Manage AWS services like DynamoDB using ACK
- Perform Day 2 operations (e.g. HPA updates)

---

## 🔧 Tech Stack & Tools

| Layer             | Tools Used                            |
|------------------|----------------------------------------|
| Cloud Platform   | AWS (EKS, DynamoDB, IAM, ELB)          |
| Kubernetes       | Amazon EKS, kubectl, Helm              |
| GitOps Engine    | ArgoCD (Hub cluster only)              |
| IaC              | Terraform                              |
| Git Repos        | GitHub (GitOps Repos), Git CLI         |
| App Delivery     | Kustomize, Helm                        |
| AWS Controllers  | ACK for DynamoDB                       |

---

## Directory Structure

```bash
.
├── terraform/                  # Infra as Code (EKS, IAM, etc.)
│   ├── hub/                    # Hub cluster setup
│   └── spokes/                 # Staging and Prod clusters
├── gitops-repos/
│   ├── platform/               # Namespaces, Addons, Argo Projects
│   └── apps/                   # Application manifests
├── install.sh                 # Bootstrap script
├── cleanup.sh                 # Clean all resources
└── README.md
