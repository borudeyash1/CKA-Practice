# 🔐 ConfigMaps, Secrets & SecurityContext (15% CKA Weight)

> **Exam Focus**: Inject configuration data and credentials via environment variables or volume mounts, and enforce security policies (non-root execution, privilege escalation) via `securityContext`.

---

## 1. ConfigMaps & Secrets Consumption

### Concept
ConfigMaps and Secrets decouple runtime configuration and credentials from container images, consuming them via `envFrom`, `valueFrom`, or `volumes`.

### Generator Command
```bash
# Imperative creation of ConfigMap and Secret
kubectl create configmap app-cfg --from-literal=LOG_LEVEL=debug --from-literal=APP_ENV=prod $do > cm.yaml
kubectl create secret generic app-sec --from-literal=API_KEY=SecretKey999 $do > sec.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: config-pod
spec:
  containers:
  - name: web
    image: nginx
    env:
    - name: LOG_LEVEL
      valueFrom:
        configMapKeyRef:
          name: app-cfg
          key: LOG_LEVEL
    - name: API_KEY
      valueFrom:
        secretKeyRef:
          name: app-sec
          key: API_KEY
    volumeMounts:
    - name: config-vol
      mountPath: /etc/config
  volumes:
  - name: config-vol
    configMap:
      name: app-cfg
```

### Verification/Debugging Command
```bash
# Inspect environment variables inside container
kubectl exec config-pod -- env | grep -E "LOG_LEVEL|API_KEY"
kubectl exec config-pod -- cat /etc/config/LOG_LEVEL
```

---

## 2. Pod & Container SecurityContext

### Concept
SecurityContext defines privilege and access control settings for a Pod or Container (Linux UID/GID, read-only root filesystems, privilege escalation prevention).

### Generator Command
```bash
# Generate baseline Pod spec
kubectl run sec-pod --image=nginx $do > sec-pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sec-demo-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  containers:
  - name: sec-container
    image: nginx
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      runAsNonRoot: true
```

### Verification/Debugging Command
```bash
# Verify UID/GID execution inside container
kubectl exec sec-demo-pod -- id
kubectl describe pod sec-demo-pod | grep -A 8 SecurityContext
```
