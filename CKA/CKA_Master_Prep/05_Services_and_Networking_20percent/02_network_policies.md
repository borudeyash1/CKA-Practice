# 🛡️ NetworkPolicies (20% CKA Weight - High Priority!)

> **Exam Focus**: Restrict ingress and egress pod traffic based on pod selectors, namespace selectors, IP CIDR blocks, and ports.

---

## 1. Ingress NetworkPolicy (Restricting Inbound Traffic)

### Concept
By default, pod network traffic is non-isolated. Applying a NetworkPolicy isolates target pods, permitting only traffic matching explicit `from` ingress rules.

### Generator Command
```bash
# NetworkPolicies must be generated via YAML templates; create template file
cat <<EOF > netpol-ingress.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-netpol
  namespace: prod
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 5432
EOF
```

### YAML Spec Snippet
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-netpol
  namespace: prod
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 5432
```

### Verification/Debugging Command
```bash
# Verify policy application and test connectivity
kubectl get netpol -n prod
kubectl describe netpol db-netpol -n prod
kubectl exec -n prod frontend-pod -- nc -zvw3 db-service 5432
```

---

## 2. Egress NetworkPolicy (Restricting Outbound Traffic)

### Concept
Egress policies restrict outbound pod traffic to specific target namespaces, pods, or external IP ranges (CIDRs).

### Generator Command
```bash
# Create Egress policy template
cat <<EOF > netpol-egress.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: app-egress-netpol
  namespace: prod
spec:
  podSelector:
    matchLabels:
      app: web
  policyTypes:
  - Egress
  egress:
  - to:
    - namespaceSelector:
        matchLabels:
          env: prod
    ports:
    - protocol: TCP
      port: 80
EOF
```

### YAML Spec Snippet
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: app-egress-netpol
  namespace: prod
spec:
  podSelector:
    matchLabels:
      app: web
  policyTypes:
  - Egress
  egress:
  - to:
    - namespaceSelector:
        matchLabels:
          env: prod
    ports:
    - protocol: TCP
      port: 80
```

### Verification/Debugging Command
```bash
# Check NetworkPolicy details
kubectl get netpol app-egress-netpol -n prod -o yaml
```
