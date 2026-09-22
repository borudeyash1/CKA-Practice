# 🤼 Multi-Container Pods, Probes, Jobs & CronJobs (15% CKA Weight)

> **Exam Focus**: Implement sidecar and init-container patterns with shared volumes, configure health probes (Liveness, Readiness, Startup), and configure batch jobs.

---

## 1. Multi-Container Pods & Sidecars

### Concept
Multi-container pods share network namespace (`localhost`) and storage volumes (`emptyDir`), enabling helper containers (log shippers, proxies) to run alongside main applications.

### Generator Command
```bash
# Generate base Pod for multi-container expansion
kubectl run multi-pod --image=busybox $do > multi-pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-demo
spec:
  volumes:
  - name: shared-logs
    emptyDir: {}
  containers:
  - name: main-app
    image: busybox
    command: ["sh", "-c", "while true; do date >> /var/log/app.log; sleep 1; done"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log
  - name: sidecar-logger
    image: busybox
    command: ["sh", "-c", "tail -f /var/log/app.log"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log
```

### Verification/Debugging Command
```bash
# View logs from specific container in multi-container pod
kubectl logs sidecar-demo -c sidecar-logger
```

---

## 2. Liveness, Readiness & Startup Probes

### Concept
Probes check application health: `readinessProbe` controls service endpoint inclusion, `livenessProbe` triggers container restarts upon failure, and `startupProbe` delays probes during slow startup.

### Generator Command
```bash
# Generate Pod template for probes
kubectl run probe-pod --image=nginx --port=80 $do > probe-pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: probe-pod
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 80
    readinessProbe:
      httpGet:
        path: /index.html
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      tcpSocket:
        port: 80
      initialDelaySeconds: 15
      periodSeconds: 20
```

### Verification/Debugging Command
```bash
# Inspect probe states and failure events
kubectl describe pod probe-pod | grep -A 10 Probes
```

---

## 3. Jobs & CronJobs

### Concept
Jobs run batch tasks to completion with completions and parallelism controls, while CronJobs run scheduled tasks using cron syntax.

### Generator Command
```bash
# Generate Job manifest
kubectl create job batch-job --image=busybox -- sh -c "echo Batch task completed" $do > job.yaml

# Generate CronJob manifest running every hour
kubectl create cronjob hourly-job --image=busybox --schedule="0 * * * *" -- date $do > cronjob.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: batch-job
spec:
  completions: 3
  parallelism: 2
  template:
    spec:
      containers:
      - name: worker
        image: busybox
        command: ["sh", "-c", "echo Working... && sleep 2"]
      restartPolicy: OnFailure
```

### Verification/Debugging Command
```bash
# Inspect Job execution and logs
kubectl get jobs
kubectl get pods -l job-name=batch-job
kubectl logs job/batch-job
```
