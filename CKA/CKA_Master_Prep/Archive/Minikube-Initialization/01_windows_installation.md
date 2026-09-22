# 🪟 Installing Minikube on Windows

## Prerequisites
- Windows 10/11 64-bit Pro, Enterprise, or Home (with WSL2 enabled).
- Virtualization enabled in BIOS.
- Container/Hypervisor driver installed (Docker Desktop or Hyper-V).

---

## Method 1: Using PowerShell (Direct Download)

```powershell
# Create target directory
New-Item -ItemType Directory -Force -Path "C:\minikube"

# Download latest minikube binary
Invoke-WebRequest -Uri "https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe" -OutFile "C:\minikube\minikube.exe"

# Add C:\minikube to User Environment PATH
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\minikube", [EnvironmentVariableTarget]::User)
```

---

## Method 2: Using Winget or Chocolatey

```powershell
# Via Winget
winget install Kubernetes.minikube

# Via Chocolatey
choco install minikube
```

---

## Method 3: Installing kubectl CLI on Windows

```powershell
# Download kubectl
Invoke-WebRequest -Uri "https://dl.k8s.io/release/v1.30.0/bin/windows/amd64/kubectl.exe" -OutFile "C:\minikube\kubectl.exe"
```

---

## Starting Minikube on Windows

```powershell
# Start using Docker Desktop driver
minikube start --driver=docker

# Start with custom profile
minikube start -p practice --driver=docker
```
