# 🚀 Minikube Initialization & Setup Guide

Minikube is a local Kubernetes engine that runs a single-node or multi-node Kubernetes cluster on your personal computer inside a Virtual Machine or Docker Container.

---

## 📑 Contents

1. [Windows Installation](file:///d:/Minikube/CKA/1-Minikube-Initialization/01_windows_installation.md)
2. [Linux Installation](file:///d:/Minikube/CKA/1-Minikube-Initialization/02_linux_installation.md)
3. [macOS Installation](file:///d:/Minikube/CKA/1-Minikube-Initialization/03_macos_installation.md)
4. [Verification & Driver Options](file:///d:/Minikube/CKA/1-Minikube-Initialization/04_verification_and_drivers.md)

---

## ⚡ Quick Start Command Summary

```bash
# 1. Start cluster with Docker driver (Recommended)
minikube start --driver=docker

# 2. Start with a specific profile name (isolated environment)
minikube start -p practice --driver=docker

# 3. Check cluster status
minikube status -p practice

# 4. Verify kubectl cluster connectivity
kubectl get nodes

# 5. Access Minikube Web Dashboard
minikube dashboard -p practice

# 6. Stop cluster
minikube stop -p practice
```
