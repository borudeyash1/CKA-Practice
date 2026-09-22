# 🍎 Installing Minikube on macOS (Intel & Apple Silicon M1/M2/M3)

## Method 1: Installing via Homebrew (Recommended)

```bash
# Install minikube and kubectl using brew
brew install minikube
brew install kubernetes-cli
```

---

## Method 2: Direct Binary Download

```bash
# macOS Intel (x86_64)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube

# macOS Apple Silicon (ARM64 M1/M2/M3)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-arm64
sudo install minikube-darwin-arm64 /usr/local/bin/minikube
```

---

## Driver Selection on macOS

1. **Docker Desktop / OrbStack Driver (Recommended)**
   ```bash
   minikube start --driver=docker
   ```

2. **HyperKit Driver (Intel Macs)**
   ```bash
   minikube start --driver=hyperkit
   ```

3. **QEMU Driver (Apple Silicon M1/M2/M3 Native)**
   ```bash
   minikube start --driver=qemu
   ```
