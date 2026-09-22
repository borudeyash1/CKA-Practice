# 🏛️ Kubernetes Fundamentals & Architecture (KCNA Domain - 46%)

## 1. Control Plane Architecture (Master Node)

The Control Plane manages the global state of the cluster, schedules workloads, and responds to cluster events.

```text
+-----------------------------------------------------------------------+
|                         CONTROL PLANE (MASTER)                        |
|                                                                       |
|  +--------------------+   +-------------------+   +----------------+  |
|  |   kube-apiserver   |---|   kube-scheduler  |---| kube-controller|  |
|  +--------------------+   +-------------------+   |    -manager    |  |
|            |                                      +----------------+  |
|  +--------------------+                                               |
|  |        etcd        |                                               |
|  +--------------------+                                               |
+-----------------------------------------------------------------------+
```

### Components Breakdown:
1. **`kube-apiserver`**:
   - The central REST API entry point for all administrative tasks and internal communication.
   - Validates and configures data for API objects (`Pods`, `Services`, `Deployments`).
   - The *only* component that communicates directly with `etcd`.

2. **`etcd`**:
   - Highly available, distributed key-value database.
   - Stores the complete cluster state and configuration.
   - Uses the Raft consensus algorithm.

3. **`kube-scheduler`**:
   - Assigns unassigned Pods to appropriate worker Nodes based on resource requirements (CPU/RAM), node selectors, taints/tolerations, and affinity rules.

4. **`kube-controller-manager`**:
   - Runs background controller loops to regulate the cluster state:
     - *Node Lifecycle Controller*: Monitors node health.
     - *ReplicaSet Controller*: Ensures correct number of pod replicas are running.
     - *Endpoints Controller*: Populates Endpoint objects (joins Services and Pods).
     - *ServiceAccount Controller*: Creates default accounts for namespaces.

5. **`cloud-controller-manager`**:
   - Interfaces Kubernetes with underlying cloud infrastructure (AWS EBS, GCP LoadBalancers, Azure VNETs).

---

## 2. Worker Node Architecture

Worker Nodes execute the actual workload containers assigned by the control plane.

```text
+-----------------------------------------------------------------------+
|                             WORKER NODE                               |
|                                                                       |
|  +--------------------+   +-------------------+   +----------------+  |
|  |      kubelet       |---|    kube-proxy     |---|Container Runtime| |
|  +--------------------+   +-------------------+   |  (containerd)  |  |
|                                                   +----------------+  |
+-----------------------------------------------------------------------+
```

1. **`kubelet`**:
   - Primary node agent. Reads `PodSpecs` provided by `kube-apiserver` and ensures matching containers are running and healthy via Container Runtime Interface (CRI).

2. **`kube-proxy`**:
   - Main networks proxy on each node. Manages IP routing rules (using `iptables` or `IPVS`) to allow network communication to Pods from inside or outside the cluster.

3. **`Container Runtime`**:
   - Underlying software responsible for running containers (e.g. `containerd`, `CRI-O`).

---

## 3. Kubernetes Object Hierarchy & Abstractions

### Workload Objects:
- **Pod**: Smallest deployable unit in Kubernetes. Contains 1 or more containers sharing network IP and storage volumes.
- **ReplicaSet**: Guarantees a specified number of running Pod replicas at any given time.
- **Deployment**: Declarative management for Pods and ReplicaSets; supports rolling updates and rollbacks.
- **StatefulSet**: Manages stateful apps requiring unique network IDs, ordered deployment, and persistent storage.
- **DaemonSet**: Ensures a copy of a Pod runs on all (or selected) worker nodes (e.g. log collectors, CNI agents).
- **Job / CronJob**: Runs short-lived batch tasks to completion / on a scheduled cron timer.

### Configuration & Storage Objects:
- **ConfigMap**: Stores non-confidential configuration key-value pairs.
- **Secret**: Stores sensitive data (passwords, tokens, keys) base64-encoded.
- **PersistentVolume (PV)**: Cluster-level storage resource provisioned by admin or dynamically.
- **PersistentVolumeClaim (PVC)**: Storage request by a user/pod to claim a PV.

---

## 4. Key Imperative kubectl Inspection Commands

```bash
# Get cluster nodes and health status
kubectl get nodes -o wide

# Check control plane component status
kubectl get componentstatuses

# Inspect all pods across all namespaces
kubectl get pods -A

# Describe node resources and events
kubectl describe node practice

# View cluster API events
kubectl get events --sort-by='.metadata.creationTimestamp'
```
