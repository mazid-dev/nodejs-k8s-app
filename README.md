# Production-Ready Node.js Application on Kubernetes with Helm

## 📋 Project Overview
This repository demonstrates an end-to-end DevOps lifecycle for deploying a production-ready, highly available Node.js application on a 3-node Kubernetes cluster using Helm charts, NGINX Ingress, HPA, Network Policies, and Prometheus Monitoring.

## 🏗️ Tech Stack & Architecture
- **Application**: Node.js (Express.js)
- **Containerization**: Docker & Docker Hub
- **Orchestration**: Kubernetes (kubeadm on VMware)
- **Packaging Tool**: Helm 3
- **Ingress Controller**: NGINX Ingress
- **Monitoring & Security**: Prometheus ServiceMonitor, NetworkPolicies, Horizontal Pod Autoscaler (HPA)

## 👥 Team & Collaboration Roles
- **Developer**: Application code development, Dockerfile optimization, local feature testing.
- **DevOps Engineer**: Kubernetes cluster setup, Helm chart templating, CI/CD pipeline automation, security policies, and ingress routing.

## 🌿 Branch Strategy
- `main` - Production-ready deployment configurations and stable releases.
- `devops` - Infrastructure manifests, Helm charts, CI/CD workflows, and security policies.
- `developer` - Core Node.js application code and Docker configurations.

## 🚀 Quick Start
1. Clone the repository:
   ```bash
   git clone [https://github.com/mazid-dev/production-ready-nodejs-k8s-helm.git](https://github.com/mazid-dev/production-ready-nodejs-k8s-helm.git)