# 🛠️ Control Plane & Worker Node Troubleshooting (30% CKA Weight)

> **Exam Focus**: Diagnose Control Plane static pods (`kube-apiserver`, `etcd`, `kube-scheduler`, `kube-controller-manager`), systemd daemon failures (`kubelet`, `containerd`), and NotReady worker nodes.

---

## 1. Control Plane Static Pod Failures

### Concept
Control plane components run as Static Pods managed directly by Kubelet reading manifests from `/etc/kubernetes/manifests/`. Errors prevent API server communication.

### Generator Command
```bash
# Check static pod manifest directory on control plane node
ls -la /etc/kubernetes/manifests/
# Key files: kube-apiserver.yaml, etcd.yaml, kube-scheduler.yaml, kube-controller-manager.yaml
```

### YAML Spec Snippet
```yaml
# Snippet from /etc/kubernetes/manifests/kube-apiserver.yaml
apiVersion: v1
kind: Pod
metadata:
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
  - command:
    - kube-apiserver
    - --advertise-address=192.168.100.10
    - --etcd-servers=https://127.0.0.1:2379
    image: registry.k8s.io/kube-apiserver:v1.30.0
    name: kube-apiserver
```

### Verification/Debugging Command
```bash
# If kubectl works, inspect static pods in kube-system
kubectl get pods -n kube-system

# If kubectl fails (API server down), use crictl directly on the host node
sudo crictl ps -a
sudo crictl logs <container-id-or-name>
sudo tail -f /var/log/pods/kube-system_kube-apiserver-*/kube-apiserver/*.log
```

---

## 2. Worker Node & Kubelet Systemd Troubleshooting

### Concept
Nodes transition to `NotReady` when `kubelet` stops running, fails to communicate with `containerd`, or experiences disk/memory pressure.

### Generator Command
```bash
# SSH into NotReady worker node and check service status
ssh node-worker-1
sudo systemctl status kubelet
sudo systemctl status containerd
```

### YAML Spec Snippet
*N/A (Systemd Daemon Diagnostics)*

### Verification/Debugging Command
```bash
# 1. Restart failed services
sudo systemctl restart containerd
sudo systemctl restart kubelet

# 2. Inspect kubelet system logs
sudo journalctl -u kubelet -n 100 --no-pager

# 3. Check kubelet configuration file syntax
cat /var/lib/kubelet/config.yaml

# 4. Confirm node status from control plane
kubectl get nodes -o wide
kubectl describe node node-worker-1 | grep -A 10 Conditions
```
