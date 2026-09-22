# 🐧 Installing Minikube on Linux (Ubuntu / Debian / RHEL)

## Prerequisites
- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Container engine (Docker, Podman, or KVM)

---

## Installation via Binary Download (x86-64 / ARM64)

```bash
# 1. Download minikube binary (x86-64)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# For ARM64 (e.g. Raspberry Pi / ARM servers):
# curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-arm64

# 2. Install minikube to /usr/local/bin
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# 3. Verify minikube version
minikube version
```

---

## Installing kubectl on Linux

```bash
# Download latest kubectl binary
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Install kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Verify kubectl
kubectl version --client
```

---

## Starting Minikube on Linux

```bash
# Ensure user is in docker group
sudo usermod -aG docker $USER && newgrp docker

# Start minikube with Docker driver
minikube start --driver=docker

# Or start rootless/kvm2 driver
minikube start --driver=kvm2
```
