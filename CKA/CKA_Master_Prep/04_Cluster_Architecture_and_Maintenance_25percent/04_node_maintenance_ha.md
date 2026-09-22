# 🧹 Node Maintenance & High Availability (25% CKA Weight)

> **Exam Focus**: Safely perform node maintenance using `cordon`, `drain`, and `uncordon`, while maintaining High Availability (HA) control plane topology.

---

## 1. Node Maintenance: Cordon, Drain & Uncordon

### Concept
`cordon` marks a node unschedulable without affecting existing pods; `drain` evicts all non-DaemonSet pods to enable host OS maintenance or rebooting.

### Generator Command
```bash
# Step 1: Mark node unschedulable
kubectl cordon node-worker-1

# Step 2: Drain all pods off node safely
kubectl drain node-worker-1 --ignore-daemonsets --delete-emptydir-data --force

# Perform maintenance / reboot...

# Step 3: Mark node schedulable again
kubectl uncordon node-worker-1
```

### YAML Spec Snippet
*N/A (CLI Node Operations)*

### Verification/Debugging Command
```bash
# Check Node SchedulingDisabled status
kubectl get nodes
kubectl describe node node-worker-1 | grep "SchedulingDisabled"
```

---

## 2. High Availability (HA) Control Plane Architecture

### Concept
HA clusters utilize 3 or more Control Plane nodes with stacked or external ETCD topology and a load balancer fronting API servers.

### Generator Command
```bash
# Initialize HA cluster with control plane endpoint
sudo kubeadm init --control-plane-endpoint "lb.example.com:6443" --upload-certs
```

### YAML Spec Snippet
*N/A (HA Initialization)*

### Verification/Debugging Command
```bash
# Check status of all control plane static pods across nodes
kubectl get pods -n kube-system -o wide | grep -E "etcd|apiserver"
```
