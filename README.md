# 🚀 Node.js Kubernetes Production Deployment

[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.30-blue)](https://kubernetes.io/)
[![Helm](https://img.shields.io/badge/Helm-v3.21-0F1689)](https://helm.sh/)
[![Docker](https://img.shields.io/badge/Docker-20.10-2496ED)](https://www.docker.com/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-339933)](https://nodejs.org/)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)]()

---

## 📋 **Project Overview**

Production-grade deployment of a **Node.js application** on a **Kubernetes cluster** (1 Master + 2 Workers) on **VMware** infrastructure with **Docker**, **Helm**, and **Ingress**.

---

## 🛠️ **Technology Stack**

| Component | Technology | Version |
|-----------|------------|---------|
| Application | Node.js (Express) | 18.x |
| Containerization | Docker | 20.10 |
| Orchestration | Kubernetes | v1.30.14 |
| Package Manager | Helm | v3.21.4 |
| CNI | Calico | v3.28.0 |
| Ingress | Nginx Ingress | v1.11.1 |
| Infrastructure | VMware (Ubuntu 24.04) | - |

---

## 🏗️ **Infrastructure**

| VM | Role | IP Address | Spec |
|----|------|------------|------|
| server1 | Master (Control Plane) | 192.168.130.129 | 4GB RAM, 2 vCPU |
| server2 | Worker Node | 192.168.130.130 | 2GB RAM, 2 vCPU |
| server3 | Worker Node | 192.168.130.131 | 2GB RAM, 2 vCPU |

---

## 🚀 **Quick Deployment**

```bash
# 1. Clone repository
sudo mkdir -p /opt/apps && sudo chown -R $USER:$USER /opt/apps
cd /opt/apps
git clone https://github.com/mazid-dev/nodejs-k8s-app.git
cd nodejs-k8s-app

# 2. Deploy with Helm
kubectl create namespace nodejs
helm install nodejs-app ./helm-chart/nodejs-app \
  --namespace nodejs \
  --set persistence.enabled=false \
  --set image.repository=mdmazidhossain77/nodejs-k8s-app \
  --set image.tag=v1.0.0
```

---

## 🧪 **Testing**

```bash
# Port Forward
kubectl port-forward -n nodejs service/nodejs-app-service 3000:80 &

# Health Check
curl http://localhost:3000/health
# {"status":"ok","uptime":123.45,"timestamp":"2026-09-03T07:05:33.678Z"}

# Application Info
curl http://localhost:3000/
# {"message":"Welcome to Node.js Kubernetes App","app":"nodejs-k8s-app",...}
```

---

## 📊 **Deployment Status**

```bash
kubectl get nodes -o wide
kubectl get pods -n nodejs -o wide
kubectl get svc -n nodejs
kubectl get ingress -n nodejs
```

**Current Status:** ✅ All pods running, application healthy

---

## 📝 **Quick Commands**

| Action | Command |
|--------|---------|
| Check Pods | `kubectl get pods -n nodejs -o wide` |
| View Logs | `kubectl logs -f -n nodejs deployment/nodejs-app` |
| Port Forward | `kubectl port-forward -n nodejs service/nodejs-app-service 3000:80` |
| Health Check | `curl http://localhost:3000/health` |

---

## 🔧 **Troubleshooting**

| Issue | Solution |
|-------|----------|
| ImagePullBackOff | Use `mdmazidhossain77/nodejs-k8s-app` |
| Port Forward Timeout | `sudo ufw allow 10250/tcp` on workers |
| Nodes NotReady | `sudo swapoff -a` |

---

## 📞 **Contact**

- **Repository:** [github.com/mazid-dev/nodejs-k8s-app](https://github.com/mazid-dev/nodejs-k8s-app)
- **Docker Image:** [hub.docker.com/r/mdmazidhossain77/nodejs-k8s-app](https://hub.docker.com/r/mdmazidhossain77/nodejs-k8s-app)

---

## 🎉 **Project Status: Production Ready ✅**

**Deployed:** September 3, 2026
