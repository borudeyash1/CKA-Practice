# 🎯 Taints, Tolerations & Node Affinity (15% CKA Weight)

> **Exam Focus**: Control Pod placement on cluster nodes using Node Selectors, Taints & Tolerations (`NoSchedule`, `NoExecute`), and Node Affinity (`required` vs `preferred`).

---

## 1. Taints & Tolerations

### Concept
Taints allow a node to repel a set of pods. Pods require matching Tolerations to be scheduled onto tainted nodes.

### Generator Command
```bash
# Apply taint to worker node imperatively
kubectl taint nodes node-worker-1 key1=value1:NoSchedule

# Remove taint from worker node imperatively
kubectl taint nodes node-worker-1 key1=value1:NoSchedule-

# Generate Pod manifest to add tolerations
kubectl run tainted-pod --image=nginx $do > pod-toleration.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: tainted-pod
spec:
  containers:
  - name: nginx
    image: nginx
  tolerations:
  - key: "key1"
    operator: "Equal"
    value: "value1"
    effect: "NoSchedule"
```

### Verification/Debugging Command
```bash
# Check taints applied on nodes
kubectl describe node node-worker-1 | grep Taints
kubectl get pod tainted-pod -o wide
```

---

## 2. NodeSelector & Node Affinity

### Concept
Node Affinity attracts Pods to specific nodes based on node labels, offering strict (`requiredDuringSchedulingIgnoredDuringExecution`) or flexible (`preferredDuringSchedulingIgnoredDuringExecution`) rules.

### Generator Command
```bash
# Label worker node imperatively
kubectl label nodes node-worker-1 disktype=ssd

# Generate base Pod for affinity insertion
kubectl run affinity-pod --image=nginx $do > pod-affinity.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: affinity-pod
spec:
  containers:
  - name: web
    image: nginx
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
```

### Verification/Debugging Command
```bash
# Verify node labels and pod scheduling target
kubectl get nodes --show-labels
kubectl get pod affinity-pod -o wide
```
