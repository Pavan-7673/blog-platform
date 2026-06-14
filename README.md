# 3-Tier Blog Platform on AWS EKS

A production-grade 3-tier web application deployed on AWS EKS using Kubernetes, Docker, and Terraform.

## Architecture## Tech Stack

| Tier | Technology |
|------|-----------|
| Frontend | HTML/CSS/JS served by nginx |
| Backend | Python Flask REST API |
| Database | MySQL 8.0 |
| Container | Docker |
| Orchestration | Kubernetes (AWS EKS) |
| Infrastructure | Terraform |
| Registry | Docker Hub |

## Kubernetes Resources Used

- Namespace
- Deployments (3 — frontend, backend, mysql)
- Services (ClusterIP for backend/mysql, LoadBalancer for frontend)
- Secrets (MySQL credentials)
- Resource Limits (CPU/memory for all pods)

## How to Deploy

### 1. Provision EKS with Terraform
```bash
cd terraform
terraform init
terraform apply
aws eks update-kubeconfig --region ap-south-1 --name ecommerce-eks-cluster
```

### 2. Deploy to Kubernetes
```bash
cd kubernetes
kubectl apply -f namespace.yaml
kubectl apply -f mysql-secret.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f backend-deployment.yaml
kubectl apply -f frontend-deployment.yaml
```

### 3. Get the App URL
```bash
kubectl get svc -n blog
```

## Docker Images

- Frontend: `pavanreddy8/blog-frontend:v1`
- Backend: `pavanreddy8/blog-backend:v1`

## Cleanup
```bash
kubectl delete namespace blog
cd terraform && terraform destroy
```
