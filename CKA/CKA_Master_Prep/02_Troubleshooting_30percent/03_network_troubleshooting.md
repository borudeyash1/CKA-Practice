# 🌐 Cluster Network & CoreDNS Troubleshooting (30% CKA Weight)

> **Exam Focus**: Resolve DNS resolution errors in `CoreDNS`, diagnose CNI plugin daemonset issues, and troubleshoot pod-to-pod and pod-to-service connectivity.

---

## 1. CoreDNS Diagnostics & Name Resolution

### Concept
CoreDNS translates cluster service names (e.g. `my-svc.my-ns.svc.cluster.local`) into ClusterIPs. Misconfigurations break internal service discovery.

### Generator Command
```bash
# Imperative run of temporary busybox pod to test internal DNS resolution
kubectl run dns-test --image=busybox:1.28 --rm -it -- restart=Never -- nslookup kubernetes.default
```

### YAML Spec Snippet
```yaml
# CoreDNS ConfigMap spec (/etc/coredns/Corefile)
apiVersion: v1
kind: ConfigMap
metadata:
  name: coredns
  namespace: kube-system
data:
  Corefile: |
    .:53 {
        errors
        health {
           lameduck 5s
        }
        ready
        kubernetes cluster.local in-addr.arpa ip6.arpa {
           pods insecure
           fallthrough in-addr.arpa ip6.arpa
           ttl 30
        }
        prometheus :9153
        forward . /etc/resolv.conf
        cache 30
        loop
        reload
        loadbalance
    }
```

### Verification/Debugging Command
```bash
# 1. Verify CoreDNS Pod status and replica count
kubectl get pods -n kube-system -l k8s-app=kube-dns

# 2. Check CoreDNS logs for upstream forwarding errors
kubectl logs -n kube-system -l k8s-app=kube-dns

# 3. Verify kube-dns Service ClusterIP matches /etc/resolv.conf inside pods
kubectl get svc -n kube-system kube-dns
```

---

## 2. CNI Plugin & Network Connectivity Troubleshooting

### Concept
Container Network Interfaces (CNI plugins like Calico, Flannel, Weave) establish virtual overlay networks, assign Pod IPs, and enforce network routing.

### Generator Command
```bash
# Check CNI config directory on worker node host
ls -la /etc/cni/net.d/
```

### YAML Spec Snippet
*N/A (Host & CNI Network Config)*

### Verification/Debugging Command
```bash
# 1. Verify CNI DaemonSet pods are Running on all nodes
kubectl get daemonset -n kube-system

# 2. Test pod-to-pod connectivity across nodes
kubectl get pods -o wide
kubectl exec -it pod-1 -- ping <pod-2-ip>

# 3. Verify node network interface status on host
ip a | grep -E "flannel|calico|weave|cni0"
```
