# ⚡ Imperative kubectl Cheatsheet & Fast-Track Generators

> **Exam Speed Strategy**: Time management is critical in CKA. Always use imperative commands with `--dry-run=client -o yaml` to generate valid YAML manifests instantly instead of writing them from scratch.

---

## 1. Shell Aliases & Speed Shortcuts

### Concept
Configure shell shortcuts in the exam environment to save typing time and avoid repetitive flags.

### Generator Command
```bash
# Add aliases to current session and ~/.bashrc
alias k=kubectl
alias kgp="kubectl get pods"
alias kgs="kubectl get svc"
alias kgd="kubectl get deployments"
alias kdp="kubectl describe pod"
alias kdd="kubectl describe deployment"
export do="--dry-run=client -o yaml"
export now="--force --grace-period=0"
```

### YAML Spec Snippet
*N/A (Shell Configuration)*

### Verification/Debugging Command
```bash
# Verify alias setup
alias k
echo $do
```

---

## 2. Pod Generators

### Concept
Imperatively generate single-container or multi-container Pod YAML manifests using `kubectl run`.

### Generator Command
```bash
# Generate single container Pod YAML manifest
kubectl run nginx-pod --image=nginx:1.25-alpine --port=80 --labels=env=prod,app=frontend $do > pod.yaml

# Generate Pod with custom command
kubectl run busy-pod --image=busybox -- command -- sh -c "echo Running... && sleep 3600" $do > pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: frontend
    env: prod
  name: nginx-pod
spec:
  containers:
  - image: nginx:1.25-alpine
    name: nginx-pod
    ports:
    - containerPort: 80
  restartPolicy: Always
```

### Verification/Debugging Command
```bash
# Apply manifest and inspect Pod status
kubectl apply -f pod.yaml
kubectl get pod nginx-pod -o wide
kubectl describe pod nginx-pod
kubectl logs nginx-pod
```

---

## 3. Deployment & Scaling Generators

### Concept
Deployments manage replicated applications with declarative updates, rolling upgrades, and auto-scaling capabilities.

### Generator Command
```bash
# Generate Deployment manifest with 3 replicas
kubectl create deployment web-app --image=nginx:1.25-alpine --replicas=3 $do > deployment.yaml

# Scale deployment imperatively
kubectl scale deployment web-app --replicas=5
```

### YAML Spec Snippet
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: web-app
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - image: nginx:1.25-alpine
        name: nginx
```

### Verification/Debugging Command
```bash
# Verify Deployment, ReplicaSet, and rollout status
kubectl get deployment web-app
kubectl get rs -l app=web-app
kubectl rollout status deployment/web-app
kubectl rollout history deployment/web-app
```

---

## 4. Service Generators

### Concept
Services provide stable network endpoints (ClusterIP, NodePort, LoadBalancer) for exposing Pod workloads inside or outside the cluster.

### Generator Command
```bash
# Expose existing Deployment as ClusterIP service
kubectl expose deployment web-app --name=web-service --port=80 --target-port=80 $do > service-clusterip.yaml

# Create NodePort service imperatively
kubectl create service nodeport web-nodeport --tcp=80:80 --nodeport=30080 $do > service-nodeport.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: ClusterIP
  selector:
    app: web-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

### Verification/Debugging Command
```bash
# Verify Service creation and target endpoints
kubectl get svc web-service
kubectl get endpoints web-service
kubectl describe svc web-service
```

---

## 5. ConfigMap & Secret Generators

### Concept
ConfigMaps store non-confidential key-value pairs, while Secrets store sensitive data (passwords, tokens, keys) in base64 format.

### Generator Command
```bash
# Create ConfigMap from literal values
kubectl create configmap app-config --from-literal=DB_HOST=mysql-svc --from-literal=DB_PORT=3306 $do > cm.yaml

# Create Secret from literal values
kubectl create secret generic app-secret --from-literal=DB_USER=admin --from-literal=DB_PASS=Secret123 $do > secret.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DB_HOST: mysql-svc
  DB_PORT: "3306"
```

### Verification/Debugging Command
```bash
# Retrieve ConfigMap data and decode Secret payload
kubectl get cm app-config -o yaml
kubectl get secret app-secret -o jsonpath='{.data.DB_PASS}' | base64 --decode; echo
```

---

## 6. Job & CronJob Generators

### Concept
Jobs execute one-off tasks to completion, while CronJobs run batch tasks on a periodic schedule.

### Generator Command
```bash
# Generate Job manifest
kubectl create job pi-calc --image=perl:5.34 -- perl -Mbignum=bpi -wle 'print bpi(500)' $do > job.yaml

# Generate CronJob manifest running every 5 minutes
kubectl create cronjob db-backup --image=busybox --schedule="*/5 * * * *" -- sh -c "date; echo Backup complete" $do > cronjob.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: db-backup
spec:
  schedule: "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: db-backup
            image: busybox
            command: ["sh", "-c", "date; echo Backup complete"]
          restartPolicy: OnFailure
```

### Verification/Debugging Command
```bash
# Monitor Jobs and CronJobs execution logs
kubectl get cronjob db-backup
kubectl get jobs --watch
kubectl logs job/pi-calc
```

---

## 7. Fast Deletion & Instant Cleanups

### Concept
Bypass normal Pod termination grace periods during exams to instantly remove stuck Pods or resources.

### Generator Command
```bash
# Force delete pod immediately
kubectl delete pod nginx-pod $now

# Delete all pods in namespace forcefully
kubectl delete pods --all -n dev $now
```

### YAML Spec Snippet
*N/A (Imperative Cleanups)*

### Verification/Debugging Command
```bash
# Confirm resource deletion
kubectl get pods -n dev
```
