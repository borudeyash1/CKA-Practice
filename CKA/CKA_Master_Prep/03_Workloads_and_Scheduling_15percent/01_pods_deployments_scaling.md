# 📦 Pods, Deployments & Rolling Updates (15% CKA Weight)

> **Exam Focus**: Manage Pod lifecycle, construct Deployments, perform zero-downtime rolling updates, record rollout history, and undo deployment revisions.

---

## 1. Deployments & Rolling Updates

### Concept
Deployments maintain desired application state, supporting zero-downtime updates via `maxSurge` and `maxUnavailable` strategies.

### Generator Command
```bash
# Generate Deployment manifest
kubectl create deployment web-deploy --image=nginx:1.24 --replicas=4 $do > deploy.yaml

# Imperative image update with history recording
kubectl set image deployment/web-deploy nginx=nginx:1.25.4 --record
```

### YAML Spec Snippet
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deploy
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
  selector:
    matchLabels:
      app: web-deploy
  template:
    metadata:
      labels:
        app: web-deploy
    spec:
      containers:
      - name: nginx
        image: nginx:1.25.4
```

### Verification/Debugging Command
```bash
# Monitor rollout progress and inspect history
kubectl rollout status deployment/web-deploy
kubectl rollout history deployment/web-deploy
```

---

## 2. Rollbacks & Revisions

### Concept
Revert deployments to previous stable revisions when newly deployed container images crash or fail health checks.

### Generator Command
```bash
# Undo deployment to previous revision
kubectl rollout undo deployment/web-deploy

# Rollback to specific historical revision
kubectl rollout undo deployment/web-deploy --to-revision=2
```

### YAML Spec Snippet
*N/A (Rollback Actions)*

### Verification/Debugging Command
```bash
# Verify deployed container image after rollback
kubectl get deployment web-deploy -o jsonpath='{.spec.template.spec.containers[0].image}'
echo ""
```
