# 🩺 Application Failure Troubleshooting (30% CKA Weight)

> **Exam Focus**: Diagnose application failure states such as `CrashLoopBackOff`, `ImagePullBackOff`, `Pending`, OOMKilled containers, and erroneous startup scripts using native debugging commands.

---

## 1. Diagnosing Pod Failure States (CrashLoopBackOff & Pending)

### Concept
Pod failures stem from misconfigured container images, failing startup commands, unresolvable PVC bindings, or insufficient node CPU/memory capacity.

### Generator Command
```bash
# Imperative pod runner with intentionally failing command for testing
kubectl run crash-pod --image=busybox -- restart=Never -- sh -c "exit 1" $do > crash-pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: crash-pod
spec:
  containers:
  - name: app
    image: busybox
    command: ["sh", "-c", "exit 1"]
  restartPolicy: Never
```

### Verification/Debugging Command
```bash
# 1. View high-level Pod phase and exit status
kubectl get pod crash-pod -o wide

# 2. Inspect Events for ImagePullBackOff or Scheduling failures
kubectl describe pod crash-pod

# 3. Retrieve current container logs
kubectl logs crash-pod

# 4. Retrieve previous instance logs if container is crash-looping
kubectl logs crash-pod --previous
```

---

## 2. Interactive Container Debugging & Shell Execution

### Concept
Execute commands directly inside running containers or attach ephemeral debug containers to diagnose file permission issues and runtime dependencies.

### Generator Command
```bash
# Imperative command to run single execution or interactive session inside Pod
kubectl exec web-pod -- printenv
kubectl exec -it web-pod -- /bin/sh
```

### YAML Spec Snippet
*N/A (Runtime Troubleshooting)*

### Verification/Debugging Command
```bash
# Execute debugging commands in specific multi-container Pod container
kubectl exec web-pod -c app-container -- curl -Iv http://localhost:8080

# Attach temporary ephemeral container for distroless image debugging
kubectl debug pod/distroless-pod -it --image=busybox --target=app-container
```

---

## 3. Resource Limits & OOMKilled Container Diagnosis

### Concept
Containers exceeding defined memory limits are terminated by the kernel Out-Of-Memory (OOM) killer with Exit Code 137.

### Generator Command
```bash
# Create Pod manifest with strict memory limits
kubectl run oom-test --image=polinux/stress $do > oom-pod.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: oom-test
spec:
  containers:
  - name: stress
    image: polinux/stress
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "250M", "--vm-hang", "1"]
    resources:
      limits:
        memory: "100Mi"
      requests:
        memory: "50Mi"
```

### Verification/Debugging Command
```bash
# Check CPU & Memory metrics of running Pods and Nodes
kubectl top pod oom-test
kubectl top nodes

# Inspect exit code 137 / OOMKilled state
kubectl describe pod oom-test | grep -i -E "OOMKilled|Exit Code"
```
