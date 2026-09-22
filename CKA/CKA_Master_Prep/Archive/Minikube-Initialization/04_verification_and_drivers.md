# 🔍 Minikube Verification & Driver Management

## Verification Checklist

Run the following commands to confirm that Minikube and Kubectl are working properly:

```bash
# 1. Check Minikube CLI version
minikube version

# 2. Check cluster status
minikube status -p practice

# 3. Verify nodes and ready state
kubectl get nodes

# 4. Verify system pods status
kubectl get pods -n kube-system

# 5. Check active kubectl context
kubectl config current-context
```

---

## 🚘 Minikube Drivers Comparison

| Driver | OS Supported | Requirements | Performance | Best For |
|---|---|---|---|---|
| `docker` | Windows, Linux, Mac | Docker Desktop / Engine | ⚡ High | Default choice for all OS |
| `hyperv` | Windows 10/11 Pro | Hyper-V enabled | 🚀 Very High | Windows enterprise dev |
| `kvm2` | Linux | libvirt / KVM | 🚀 Very High | Native Linux virtualization |
| `qemu` | macOS ARM (M1/M2/M3) | QEMU package | ⚡ High | Apple Silicon native |
| `virtualbox` | Windows, Linux, Mac | VirtualBox 6.x/7.x | 🐢 Medium | Legacy virtualization |

---

## 🛠️ Essential Cluster Lifecycle Commands

```bash
# Start cluster with specific profile
minikube start -p practice --driver=docker --cpus=2 --memory=4096

# Pause cluster (frees CPU without losing state)
minikube pause -p practice

# Unpause cluster
minikube unpause -p practice

# Stop cluster node gracefully
minikube stop -p practice

# Delete profile & clear Docker resources
minikube delete -p practice
```
