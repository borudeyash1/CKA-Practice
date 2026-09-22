# ⬆️ Kubeadm Cluster Upgrade Process (25% CKA Weight)

> **Exam Focus**: Safely upgrade a Kubernetes cluster using `kubeadm`, upgrading Control Plane nodes first followed by Worker nodes, managing package holds, node draining, and component restarts.

---

## 1. Upgrading Control Plane Node

### Concept
Upgrading control plane nodes requires unholding `kubeadm`, planning the upgrade, applying the upgrade, draining the node, and updating `kubelet` and `kubectl`.

### Generator Command
```bash
# Step 1: Unhold and update kubeadm package on control plane
sudo apt-mark unhold kubeadm && sudo apt-get update
sudo apt-get install -y kubeadm=1.30.0-1.1
sudo apt-mark hold kubeadm

# Step 2: Verify upgrade plan and apply
sudo kubeadm upgrade plan
sudo kubeadm upgrade apply v1.30.0 -y

# Step 3: Drain control plane node
kubectl drain controlplane --ignore-daemonsets --delete-emptydir-data

# Step 4: Upgrade kubelet and kubectl
sudo apt-mark unhold kubelet kubectl
sudo apt-get install -y kubelet=1.30.0-1.1 kubectl=1.30.0-1.1
sudo apt-mark hold kubelet kubectl

# Step 5: Reload systemd & restart kubelet, then uncordon node
sudo systemctl daemon-reload
sudo systemctl restart kubelet
kubectl uncordon controlplane
```

### YAML Spec Snippet
*N/A (Cluster Upgrade CLI Operations)*

### Verification/Debugging Command
```bash
# Verify control plane node version
kubectl get nodes
kubeadm version
```

---

## 2. Upgrading Worker Nodes

### Concept
Worker node upgrades involve upgrading `kubeadm`, running `kubeadm upgrade node`, draining workload pods, updating `kubelet`/`kubectl`, restarting `kubelet`, and uncordoning.

### Generator Command
```bash
# Step 1: From control plane, drain worker node
kubectl drain node-1 --ignore-daemonsets --delete-emptydir-data

# Step 2: On worker node (node-1), upgrade kubeadm
sudo apt-mark unhold kubeadm && sudo apt-get update
sudo apt-get install -y kubeadm=1.30.0-1.1
sudo apt-mark hold kubeadm

# Step 3: Execute node upgrade configuration
sudo kubeadm upgrade node

# Step 4: Upgrade kubelet & kubectl on worker node
sudo apt-mark unhold kubelet kubectl
sudo apt-get install -y kubelet=1.30.0-1.1 kubectl=1.30.0-1.1
sudo apt-mark hold kubelet kubectl
sudo systemctl daemon-reload && sudo systemctl restart kubelet

# Step 5: From control plane, uncordon worker node
kubectl uncordon node-1
```

### YAML Spec Snippet
*N/A (Worker Upgrade CLI Operations)*

### Verification/Debugging Command
```bash
# Confirm all nodes match target version
kubectl get nodes -o wide
```
