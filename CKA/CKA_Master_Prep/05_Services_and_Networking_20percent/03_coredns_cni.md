# 🔌 CoreDNS Architecture & CNI Plugins (20% CKA Weight)

> **Exam Focus**: Understand CoreDNS resolution chains, cluster domain extensions, and CNI network plugin installation and configuration.

---

## 1. CoreDNS Configuration & Custom DNS Records

### Concept
CoreDNS configuration is managed via the `coredns` ConfigMap in `kube-system`. Custom upstream resolvers and stub domains are added inside the `Corefile` block.

### Generator Command
```bash
# Export existing CoreDNS ConfigMap
kubectl get cm coredns -n kube-system -o yaml > coredns-cm.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: coredns
  namespace: kube-system
data:
  Corefile: |
    .:53 {
        errors
        health
        ready
        kubernetes cluster.local in-addr.arpa ip6.arpa {
           pods insecure
           fallthrough in-addr.arpa ip6.arpa
        }
        prometheus :9153
        forward . 8.8.8.8 1.1.1.1
        cache 30
        loop
        reload
        loadbalance
    }
```

### Verification/Debugging Command
```bash
# Restart CoreDNS rollout after editing ConfigMap
kubectl rollout restart deployment coredns -n kube-system
kubectl get pods -n kube-system -l k8s-app=kube-dns
```

---

## 2. CNI Network Plugins (Flannel, Calico)

### Concept
CNI plugins configure pod network interfaces (veth pairs), assign IP addresses from host-local subnet pools, and manage node routing tables.

### Generator Command
```bash
# Imperative deployment of CNI plugin (e.g. Calico / Flannel)
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.1/manifests/calico.yaml
```

### YAML Spec Snippet
*N/A (Third-party CNI Operator Manifest)*

### Verification/Debugging Command
```bash
# Verify CNI plugin pod readiness across all cluster nodes
kubectl get pods -n kube-system -o wide | grep -E "calico|flannel|weave"
cat /etc/cni/net.d/10-flannel.conflist
```
