# ⚡ KCNA High-Yield Smart Revision & Flashcard Cheat Sheet

This rapid revision cheat sheet contains **must-know ports, API groups, CNCF project mappings, and high-frequency exam terms**. Review this file during Days 10, 19, and 20!

---

## 📌 1. Essential Port Numbers (Must Memorize!)

| Component | Default Port | Description |
|---|---|---|
| **kube-apiserver** | `6443` | Control plane API server REST endpoint |
| **etcd client** | `2379` | Key-value store client communication |
| **etcd peer** | `2380` | etcd cluster node-to-node synchronization |
| **kubelet** | `10250` | Node agent API endpoint |
| **kube-scheduler** | `10259` | Secure scheduler metrics & health |
| **kube-controller-manager** | `10257` | Secure controller manager endpoint |
| **NodePort range** | `30000-32767` | Range reserved for NodePort services |
| **Prometheus metrics** | `9090` | Prometheus web UI / metrics server |
| **CoreDNS** | `53` (UDP/TCP) | Cluster internal DNS service |

---

## 📌 2. Core Kubernetes API Groups

| API Group | Key Objects |
|---|---|
| **Core (`""` or `v1`)** | `Pod`, `Service`, `ConfigMap`, `Secret`, `Namespace`, `Node`, `PersistentVolume`, `PersistentVolumeClaim` |
| **`apps/v1`** | `Deployment`, `ReplicaSet`, `StatefulSet`, `DaemonSet` |
| **`batch/v1`** | `Job`, `CronJob` |
| **`networking.k8s.io/v1`** | `Ingress`, `NetworkPolicy` |
| **`storage.k8s.io/v1`** | `StorageClass` |
| **`rbac.authorization.k8s.io/v1`** | `Role`, `ClusterRole`, `RoleBinding`, `ClusterRoleBinding` |

---

## 📌 3. CNCF Project Landscape Quick Map

### 🟢 Graduated Projects (Highest Maturity & Adoption):
- **Orchestration**: `Kubernetes`
- **Monitoring & Metrics**: `Prometheus`
- **Proxy & Service Mesh**: `Envoy`
- **Container Runtimes**: `containerd`
- **Package Manager**: `Helm`
- **GitOps Continuous Delivery**: `ArgoCD`
- **Tracing**: `Jaeger`
- **Logging**: `Fluentd`
- **Runtime Security**: `Falco`

### 🟡 Incubating Projects (Growing Adoption):
- **Policy Engine**: `Kyverno`, `OPA (Open Policy Agent)`
- **Vulnerability Scanner**: `Trivy`
- **Serverless Autoscaler**: `KEDA`
- **Persistent Storage**: `Rook`, `Longhorn`
- **Tracing / Telemetry**: `OpenTelemetry`
- **Service Mesh**: `Linkerd`

---

## 📌 4. Storage Access Modes Cheat Table

| Access Mode | Code | Description | Example Volume |
|---|---|---|---|
| **ReadWriteOnce** | `RWO` | Mounted as read-write by a **single** node | AWS EBS, GCP Persistent Disk |
| **ReadOnlyMany** | `ROX` | Mounted as read-only by **many** nodes | Shared NFS read-only |
| **ReadWriteMany** | `RWX` | Mounted as read-write by **many** nodes | NFS, CephFS, GlusterFS |
| **ReadWriteOncePod** | `RWOP` | Mounted as read-write by a **single Pod** across cluster | Single-pod exclusive disk |

---

## 📌 5. Prometheus 4 Metric Types

1. **Counter**: Only goes UP or resets to 0 (e.g. `http_requests_total`). Use `rate()` or `increase()`.
2. **Gauge**: Goes UP and DOWN (e.g. `node_memory_active_bytes`, `process_cpu_threads`).
3. **Histogram**: Measures duration/sizes into cumulative **buckets** (e.g. `http_request_duration_seconds_bucket`).
4. **Summary**: Calculates configurable **quantiles** (e.g. `phi=0.99` for 99th percentile latency).

---

## 📌 6. 12-Factor App & Cloud Native Principles Flashcard

- **Factor III (Config)**: Store configuration in environment variables (`ConfigMap`/`Secret`).
- **Factor VI (Processes)**: Execute app as stateless, share-nothing processes.
- **Factor XI (Logs)**: Treat logs as unbuffered event streams sent to `stdout`/`stderr`.
- **GitOps Core Principle**: Git repository as the **Single Source of Truth** with automated reconciliation.
- **Service Mesh Sidecar**: **Envoy** proxy deployed alongside application container to handle mTLS and telemetry without modifying application code.
