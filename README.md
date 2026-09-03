# 🚀 Node.js Kubernetes Production Deployment

[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.30-blue)](https://kubernetes.io/)
[![Helm](https://img.shields.io/badge/Helm-v3.21-0F1689)](https://helm.sh/)
[![Docker](https://img.shields.io/badge/Docker-20.10-2496ED)](https://www.docker.com/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-339933)](https://nodejs.org/)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)]()

---

## 📋 **Project Overview**

Production-grade deployment of a **Node.js application** on a **Kubernetes cluster** (1 Master + 2 Workers) on **VMware** infrastructure with **Docker**, **Helm**, and **Ingress**.

### 🎯 **What This Project Does**
- Deploys a Node.js Express API with health checks
- Runs on a 3-node Kubernetes cluster
- Auto-heals with Liveness & Readiness probes
- Scales with 2 replicas for high availability

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

### Prerequisites
- Kubernetes cluster (1 Master + 2 Workers)
- Helm installed
- kubectl configured

### Step 1: Clone Repository
```bash
sudo mkdir -p /opt/apps && sudo chown -R $USER:$USER /opt/apps
cd /opt/apps
git clone https://github.com/mazid-dev/nodejs-k8s-app.git
cd nodejs-k8s-app
```

### Step 2: Deploy with Helm
```bash
# Create namespace
kubectl create namespace nodejs

# Deploy application
helm install nodejs-app ./helm-chart/nodejs-app \
  --namespace nodejs \
  --set persistence.enabled=false \
  --set image.repository=mdmazidhossain77/nodejs-k8s-app \
  --set image.tag=v1.0.0
```

### Step 3: Verify Deployment
```bash
kubectl get pods -n nodejs -o wide
kubectl get svc -n nodejs
kubectl get ingress -n nodejs
```

---

## 🧪 **Testing Your Application**

### Access via Port Forward
```bash
# Forward port
kubectl port-forward -n nodejs service/nodejs-app-service 3000:80 &

# Health Check
curl http://localhost:3000/health
```

**Expected Output:**
```json
{
  "status": "ok",
  "uptime": 123.45,
  "timestamp": "2026-09-03T07:05:33.678Z"
}
```

### Access via Ingress
```bash
# Add to /etc/hosts
echo "192.168.130.129 nodejs-app.local" | sudo tee -a /etc/hosts

# Test
curl http://nodejs-app.local/health
```

### Access via NodePort
```bash
# Change service type
kubectl patch svc nodejs-app-service -n nodejs -p '{"spec":{"type":"NodePort"}}'

# Get NodePort
kubectl get svc -n nodejs

# Access
curl http://192.168.130.130:30001/health
```

---

## 📊 **Deployment Status**

```bash
kubectl get nodes -o wide
kubectl get pods -n nodejs -o wide
kubectl get svc -n nodejs
kubectl get ingress -n nodejs
```

**✅ Current Status: All pods running, application healthy**

---

## 📝 **Quick Commands Reference**

| Action | Command |
|--------|---------|
| **Check Pods** | `kubectl get pods -n nodejs -o wide` |
| **View Logs** | `kubectl logs -f -n nodejs deployment/nodejs-app` |
| **Port Forward** | `kubectl port-forward -n nodejs service/nodejs-app-service 3000:80` |
| **Health Check** | `curl http://localhost:3000/health` |
| **Application Info** | `curl http://localhost:3000/` |
| **Describe Pod** | `kubectl describe pod -n nodejs <pod-name>` |
| **View Events** | `kubectl get events -n nodejs --sort-by='.lastTimestamp'` |

---

## 🔧 **Troubleshooting Guide**

| Issue | Solution |
|-------|----------|
| **ImagePullBackOff** | Use correct repository: `mdmazidhossain77/nodejs-k8s-app` |
| **Port Forward Timeout** | Allow kubelet port: `sudo ufw allow 10250/tcp` on workers |
| **Node NotReady** | Disable swap: `sudo swapoff -a` |
| **Ingress 404** | Check Ingress Controller: `kubectl get pods -n ingress-nginx` |
| **Pod CrashLoopBackOff** | Check logs: `kubectl logs -n nodejs <pod-name>` |

---

## 🔒 **Security Features**

- ✅ **Non-root User** - Container runs as `nodejs` user
- ✅ **Resource Limits** - CPU/Memory constraints
- ✅ **Health Checks** - Auto-recovery on failure
- ✅ **Secrets** - Managed via Kubernetes Secrets
- ✅ **Network Policy** - Calico CNI for security

---

## 📈 **Performance Metrics**

| Metric | Value |
|--------|-------|
| **Image Size** | 45.6 MB |
| **Memory Usage** | 128-256 MiB per pod |
| **CPU Usage** | 100-200m per pod |
| **Replicas** | 2 (High Availability) |


---

## 📞 **Resources**

- **GitHub:** [github.com/mazid-dev/nodejs-k8s-app](https://github.com/mazid-dev/nodejs-k8s-app)
- **Docker Hub:** [hub.docker.com/r/mdmazidhossain77/nodejs-k8s-app](https://hub.docker.com/r/mdmazidhossain77/nodejs-k8s-app)
- **Issues:** [GitHub Issues](https://github.com/mazid-dev/nodejs-k8s-app/issues)

---

## 🎉 **Project Status**

| Detail | Value |
|--------|-------|
| **Status** | ✅ Production Ready |
| **Deployed** | September 3, 2026 |
| **Health** | ✅ All pods running |

---

**🚀 Successfully deployed a production-grade Node.js application on Kubernetes with health checks, ingress, and high availability!**
