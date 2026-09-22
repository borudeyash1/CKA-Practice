# 🎯 KCNA Master Practice Exam (50 Exam-Style Questions with ✅/❌ Validation)

Welcome to the KCNA Master Practice Exam. This question bank contains **50 realistic exam questions** covering all 5 CNCF curriculum domains. 

Click **`🔍 Reveal Answer & Validation`** under each question to inspect detailed tick mark ✅ and cross mark ❌ explanations.

---

## 📑 Domain Map
- [Domain 1: Kubernetes Fundamentals (Q1 - Q23)](#domain-1-kubernetes-fundamentals)
- [Domain 2: Container Orchestration (Q24 - Q34)](#domain-2-container-orchestration)
- [Domain 3: Cloud Native Architecture (Q35 - Q42)](#domain-3-cloud-native-architecture)
- [Domain 4: Cloud Native Observability (Q43 - Q46)](#domain-4-cloud-native-observability)
- [Domain 5: Cloud Native Application Delivery (Q47 - Q50)](#domain-5-cloud-native-application-delivery)

---

## Domain 1: Kubernetes Fundamentals

### Q1. Which control plane component is the ONLY component that reads and writes directly to the etcd database?
- [ ] A) kube-scheduler
- [ ] B) kube-controller-manager
- [ ] C) kube-apiserver
- [ ] D) kubelet

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) kube-scheduler**: Incorrect. The scheduler queries node resources through `kube-apiserver`.
- ❌ **B) kube-controller-manager**: Incorrect. Controllers monitor cluster state strictly via `kube-apiserver`.
- ✅ **C) kube-apiserver**: **CORRECT!** The `kube-apiserver` is the sole control plane gateway authorized to communicate directly with `etcd`.
- ❌ **D) kubelet**: Incorrect. `kubelet` is a worker node agent and only talks to `kube-apiserver`.
</details>

---

### Q2. Which Kubernetes object guarantees that a specified number of Pod replicas are running at any given time?
- [ ] A) DaemonSet
- [ ] B) ReplicaSet
- [ ] C) Job
- [ ] D) StatefulSet

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) DaemonSet**: Incorrect. Runs one copy of a pod per matching node, but doesn't handle arbitrary replica scaling.
- ✅ **B) ReplicaSet**: **CORRECT!** A `ReplicaSet`'s core purpose is maintaining a stable number of running Pod replicas.
- ❌ **C) Job**: Incorrect. Runs pods to batch completion.
- ❌ **D) StatefulSet**: Incorrect. Used for ordered, stateful apps requiring stable network identities.
</details>

---

### Q3. A developer needs to run a logging agent pod on EVERY node in the cluster. Which workload resource should they use?
- [ ] A) Deployment
- [ ] B) StatefulSet
- [ ] C) DaemonSet
- [ ] D) CronJob

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Deployment**: Incorrect. Distributes pods dynamically, not guaranteed 1-per-node.
- ❌ **B) StatefulSet**: Incorrect. Used for ordered stateful pods (databases).
- ✅ **C) DaemonSet**: **CORRECT!** A `DaemonSet` ensures that all (or matching) worker nodes run a copy of a Pod (ideal for node monitoring & log collection).
- ❌ **D) CronJob**: Incorrect. Runs batch tasks on cron schedule.
</details>

---

### Q4. Which default TCP port does `kube-apiserver` listen on for secure client REST communication?
- [ ] A) 2379
- [ ] B) 6443
- [ ] C) 10250
- [ ] D) 8080

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) 2379**: Incorrect. Port 2379 is used by `etcd`.
- ✅ **B) 6443**: **CORRECT!** `kube-apiserver` listens on port `6443` by default.
- ❌ **C) 10250**: Incorrect. Port 10250 is used by `kubelet`.
- ❌ **D) 8080**: Incorrect. Legacy unencrypted HTTP port (now deprecated/removed).
</details>

---

### Q5. What API group does the `Deployment` resource belong to in Kubernetes API?
- [ ] A) `v1` (Core)
- [ ] B) `apps/v1`
- [ ] C) `batch/v1`
- [ ] D) `extensions/v1beta1`

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) v1**: Incorrect. Core `v1` group contains Pods, Services, ConfigMaps, Secrets.
- ✅ **B) apps/v1**: **CORRECT!** `Deployment`, `ReplicaSet`, `StatefulSet`, and `DaemonSet` belong to the `apps/v1` API group.
- ❌ **C) batch/v1**: Incorrect. Contains `Job` and `CronJob`.
- ❌ **D) extensions/v1beta1**: Incorrect. Deprecated legacy group.
</details>

---

### Q6. Which component is responsible for assigning an unscheduled Pod to an appropriate worker node based on CPU/RAM requests?
- [ ] A) kube-controller-manager
- [ ] B) kube-scheduler
- [ ] C) kube-proxy
- [ ] D) coredns

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) kube-controller-manager**: Incorrect. Regulates cluster state controllers.
- ✅ **B) kube-scheduler**: **CORRECT!** The `kube-scheduler` evaluates node capacity, taints, and affinity rules to select nodes for unscheduled pods.
- ❌ **C) kube-proxy**: Incorrect. Manages network proxy rules.
- ❌ **D) coredns**: Incorrect. Handles internal cluster DNS lookup.
</details>

---

### Q7. You need to store sensitive database passwords in Kubernetes. Which resource should you use?
- [ ] A) ConfigMap
- [ ] B) PersistentVolume
- [ ] C) Secret
- [ ] D) ServiceAccount

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) ConfigMap**: Incorrect. ConfigMaps store non-sensitive configuration data.
- ❌ **B) PersistentVolume**: Incorrect. PVs represent cluster storage space.
- ✅ **C) Secret**: **CORRECT!** `Secrets` are designed specifically to store sensitive data like passwords, API keys, and SSH keys.
- ❌ **D) ServiceAccount**: Incorrect. ServiceAccounts provide identities for Pods.
</details>

---

### Q8. What type of database is `etcd` in Kubernetes?
- [ ] A) Relational SQL Database
- [ ] B) Document MongoDB Database
- [ ] C) Distributed Key-Value Store
- [ ] D) Graph Database

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Relational SQL**: Incorrect.
- ❌ **B) Document Database**: Incorrect.
- ✅ **C) Distributed Key-Value Store**: **CORRECT!** `etcd` is a strongly consistent, distributed key-value store using the Raft consensus algorithm.
- ❌ **D) Graph Database**: Incorrect.
</details>

---

### Q9. What is the default Service type if no type is explicitly specified in a Service YAML manifest?
- [ ] A) NodePort
- [ ] B) LoadBalancer
- [ ] C) ClusterIP
- [ ] D) ExternalName

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) NodePort**: Incorrect.
- ❌ **B) LoadBalancer**: Incorrect.
- ✅ **C) ClusterIP**: **CORRECT!** `ClusterIP` is the default service type, making the service accessible only internally inside the cluster.
- ❌ **D) ExternalName**: Incorrect.
</default>

---

### Q10. What port range is reserved by default in Kubernetes for `NodePort` Services?
- [ ] A) 80-443
- [ ] B) 10250-10259
- [ ] C) 30000-32767
- [ ] D) 6443-8443

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) 80-443**: Incorrect. Standard HTTP/HTTPS ports.
- ❌ **B) 10250-10259**: Incorrect. System control plane/kubelet ports.
- ✅ **C) 30000-32767**: **CORRECT!** Kubernetes reserves ports `30000-32767` for NodePort services.
- ❌ **D) 6443-8443**: Incorrect. API server/webhook ports.
</details>

---

### Q11. Which object provides virtual isolation within a single physical Kubernetes cluster?
- [ ] A) ClusterRole
- [ ] B) Namespace
- [ ] C) CustomResourceDefinition
- [ ] D) NodeGroup

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) ClusterRole**: Incorrect. RBAC role object.
- ✅ **B) Namespace**: **CORRECT!** `Namespaces` provide virtual isolation boundaries for resources within a shared physical cluster.
- ❌ **C) CustomResourceDefinition**: Incorrect. Extends Kubernetes API.
- ❌ **D) NodeGroup**: Incorrect. Cloud provider node grouping.
</details>

---

### Q12. You run `kubectl get pods` and a pod shows `CrashLoopBackOff`. What does this indicate?
- [ ] A) The pod is waiting for a node assignment from the scheduler.
- [ ] B) The container keeps failing, terminating, and restarting repeatedly with exponential backoff delays.
- [ ] C) The container image cannot be pulled from the registry.
- [ ] D) The pod is performing a successful database migration.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Pending state**: Incorrect.
- ✅ **B) Repeated Failure**: **CORRECT!** `CrashLoopBackOff` means a container process exits/crashes repeatedly, so Kubernetes waits progressively longer before restarting it.
- ❌ **C) ErrImagePull**: Incorrect. Image pull failures result in `ImagePullBackOff`.
- ❌ **D) Migration**: Incorrect.
</details>

---

### Q13. Which object exposes HTTP/HTTPS routes from outside the cluster to internal Services based on host or path rules?
- [ ] A) Egress
- [ ] B) Ingress
- [ ] C) NodePort
- [ ] D) CoreDNS

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Egress**: Incorrect. Egress handles outbound traffic rules.
- ✅ **B) Ingress**: **CORRECT!** `Ingress` manages HTTP/HTTPS routing rules into internal cluster services based on hostname or URL paths.
- ❌ **C) NodePort**: Incorrect. Low-level L4 service port exposure.
- ❌ **D) CoreDNS**: Incorrect. Handles internal cluster DNS.
</details>

---

### Q14. Which field in a Pod definition ensures that a container runs as a non-root user ID?
- [ ] A) `nodeSelector`
- [ ] B) `securityContext`
- [ ] C) `serviceAccountName`
- [ ] D) `tolerations`

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) nodeSelector**: Incorrect. Schedules pod to matching node labels.
- ✅ **B) securityContext**: **CORRECT!** `securityContext` specifies privilege and access control settings (e.g. `runAsUser: 1000`, `runAsNonRoot: true`).
- ❌ **C) serviceAccountName**: Incorrect. Specifies pod service identity.
- ❌ **D) tolerations**: Incorrect. Allows pod to schedule on tainted nodes.
</details>

---

### Q15. What object is created by a user or application to request persistent storage from Kubernetes?
- [ ] A) StorageClass
- [ ] B) PersistentVolumeClaim (PVC)
- [ ] C) VolumeMount
- [ ] D) PersistentVolume (PV)

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) StorageClass**: Incorrect. Defines the dynamic storage provisioner and parameters.
- ✅ **B) PVC**: **CORRECT!** A `PersistentVolumeClaim` (PVC) is a request for storage by a user/pod.
- ❌ **C) VolumeMount**: Incorrect. Specifies mount path inside container filesystem.
- ❌ **D) PV**: Incorrect. PV is the actual underlying storage resource provided by admin/provisioner.
</details>

---

## Domain 2: Container Orchestration (Questions 24 - 34)

### Q24. Which specification standardizes the interface between `kubelet` and container runtimes?
- [ ] A) OCI (Open Container Initiative)
- [ ] B) CNI (Container Network Interface)
- [ ] C) CRI (Container Runtime Interface)
- [ ] D) CSI (Container Storage Interface)

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) OCI**: Incorrect. Governs container image and runtime format specs.
- ❌ **B) CNI**: Incorrect. Governs container networking plugins.
- ✅ **C) CRI**: **CORRECT!** `CRI` (Container Runtime Interface) defines the gRPC interface enabling `kubelet` to use runtimes like containerd or CRI-O.
- ❌ **D) CSI**: Incorrect. Governs storage volume plugins.
</details>

---

### Q25. Which container runtime is a low-level OCI runtime responsible for directly interacting with Linux kernel namespaces and cgroups to spawn container processes?
- [ ] A) containerd
- [ ] B) runc
- [ ] C) CRI-O
- [ ] D) Docker Engine

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) containerd**: Incorrect. High-level runtime manager.
- ✅ **B) runc**: **CORRECT!** `runc` is the OCI reference low-level runtime that creates container processes directly in Linux kernel.
- ❌ **C) CRI-O**: Incorrect. High-level Kubernetes runtime.
- ❌ **D) Docker Engine**: Incorrect. Developer application suite.
</details>

---

### Q26. Which CNI plugin leverages Linux eBPF (Extended Berkeley Packet Filter) technology to replace traditional iptables overhead for high-performance networking and security?
- [ ] A) Flannel
- [ ] B) Cilium
- [ ] C) Weave Net
- [ ] D) Kube-router

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Flannel**: Incorrect. Simple VXLAN overlay network without policy engine.
- ✅ **B) Cilium**: **CORRECT!** `Cilium` uses Linux eBPF for transparent, high-performance L3-L7 networking and security enforcement.
- ❌ **C) Weave Net**: Incorrect. Traditional mesh overlay network.
- ❌ **D) Kube-router**: Incorrect. BGP/IPVS based network router.
</details>

---

### Q27. Which PersistentVolume AccessMode allows a volume to be mounted as read-write by multiple nodes simultaneously?
- [ ] A) ReadWriteOnce (RWO)
- [ ] B) ReadOnlyMany (ROX)
- [ ] C) ReadWriteMany (RWX)
- [ ] D) ReadWriteOncePod (RWOP)

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) RWO**: Incorrect. Mounted as read-write by a single node.
- ❌ **B) ROX**: Incorrect. Mounted as read-only by multiple nodes.
- ✅ **C) RWX**: **CORRECT!** `ReadWriteMany` (RWX) allows the volume to be mounted as read-write by many nodes simultaneously (e.g. NFS, CephFS).
- ❌ **D) RWOP**: Incorrect. Mounted as read-write by a single Pod across the entire cluster.
</details>

---

## Domain 3: Cloud Native Architecture (Questions 35 - 42)

### Q35. According to Cloud Native principles, how should application configurations be handled?
- [ ] A) Hardcoded inside source code binaries.
- [ ] B) Injected via environment variables or external ConfigMaps/Secrets.
- [ ] C) Stored on a shared local disk on the master node.
- [ ] D) Re-compiled into Dockerfile layers per deployment.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Hardcoded**: Incorrect. Violates 12-factor principles.
- ✅ **B) Environment vars / ConfigMaps**: **CORRECT!** Cloud Native 12-Factor principles dictate strict separation of configuration from application code.
- ❌ **C) Shared disk**: Incorrect. Violates stateless architecture.
- ❌ **D) Dockerfile layers**: Incorrect. Antip-pattern to rebuild container images for configuration changes.
</details>

---

### Q36. In a Service Mesh architecture (e.g., Istio, Linkerd), what component intercepts and manages network traffic for application microservices?
- [ ] A) Control plane controller
- [ ] B) Ingress Gateway
- [ ] C) Sidecar proxy (e.g., Envoy)
- [ ] D) CoreDNS pod

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Control plane**: Incorrect. Configures proxies, but doesn't handle inline proxy traffic.
- ❌ **B) Ingress Gateway**: Incorrect. Handles entry into the cluster mesh, not inter-service sidecar traffic.
- ✅ **C) Sidecar proxy (Envoy)**: **CORRECT!** Sidecar proxies (e.g. Envoy) run alongside application containers to transparently handle mTLS, routing, and telemetry.
- ❌ **D) CoreDNS**: Incorrect. Internal cluster DNS.
</details>

---

### Q37. Which CNCF project maturity level represents the highest tier of production readiness, governance, and enterprise adoption?
- [ ] A) Sandbox
- [ ] B) Incubating
- [ ] C) Graduated
- [ ] D) Enterprise

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Sandbox**: Incorrect. Early-stage experimental projects.
- ❌ **B) Incubating**: Incorrect. Production ready with growing adoption.
- ✅ **C) Graduated**: **CORRECT!** `Graduated` is the highest CNCF maturity level (e.g. Kubernetes, Prometheus, Envoy, containerd, Helm, ArgoCD).
- ❌ **D) Enterprise**: Incorrect. Non-existent CNCF tier name.
</details>

---

## Domain 4: Cloud Native Observability (Questions 43 - 46)

### Q43. Which metric type in Prometheus represents a single numerical value that can go up and down (such as memory usage)?
- [ ] A) Counter
- [ ] B) Gauge
- [ ] C) Histogram
- [ ] D) Summary

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Counter**: Incorrect. Counters can only increase or reset to 0.
- ✅ **B) Gauge**: **CORRECT!** A `Gauge` represents a single numerical value that can arbitrarily go up or down (e.g. CPU/RAM usage, temperature).
- ❌ **C) Histogram**: Incorrect. Measures observations into cumulative buckets.
- ❌ **D) Summary**: Incorrect. Calculates quantiles over sliding time windows.
</details>

---

### Q44. How does the Prometheus server collect metrics from target applications by default?
- [ ] A) Applications push logs via SSH to Prometheus.
- [ ] B) Prometheus uses a Pull model by scraping HTTP GET `/metrics` endpoints.
- [ ] C) Prometheus polls Linux kernel sysinfo directly.
- [ ] D) Applications write metrics to etcd.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Push via SSH**: Incorrect.
- ✅ **B) Pull model `/metrics`**: **CORRECT!** Prometheus periodically scrapes (pulls) metrics from HTTP `/metrics` endpoints exposed by application targets.
- ❌ **C) Kernel sysinfo**: Incorrect.
- ❌ **D) Write to etcd**: Incorrect.
</details>

---

### Q45. Which observability component tracks a request transaction end-to-end across multiple microservice boundaries using Trace IDs?
- [ ] A) Fluentd
- [ ] B) Jaeger (Distributed Tracing)
- [ ] C) Prometheus
- [ ] D) Grafana Loki

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Fluentd**: Incorrect. Log collector agent.
- ✅ **B) Jaeger**: **CORRECT!** `Jaeger` provides distributed tracing to monitor transaction requests across microservices using Trace IDs.
- ❌ **C) Prometheus**: Incorrect. Metrics monitoring system.
- ❌ **D) Grafana Loki**: Incorrect. Log aggregation system.
</details>

---

## Domain 5: Cloud Native Application Delivery (Questions 47 - 50)

### Q47. What is the core principle of GitOps?
- [ ] A) Managing cluster operations through manual SSH terminal commands.
- [ ] B) Using Git repositories as the single source of truth for declarative infrastructure and application state.
- [ ] C) Storing container images inside Git repositories.
- [ ] D) Running manual deployment scripts from local laptops.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Manual SSH**: Incorrect. Anti-pattern in GitOps.
- ✅ **B) Git as Single Source of Truth**: **CORRECT!** GitOps relies on Git repositories as the single declarative source of truth for infrastructure and app configurations with automated reconciliation agents (ArgoCD/Flux).
- ❌ **C) Container images in Git**: Incorrect. Images are stored in container registries.
- ❌ **D) Manual scripts**: Incorrect. Anti-pattern.
</details>

---

### Q48. Which file in a Helm Chart holds the default configuration variables for deployment templates?
- [ ] A) `Chart.yaml`
- [ ] B) `values.yaml`
- [ ] C) `templates/deployment.yaml`
- [ ] D) `Chart.lock`

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Chart.yaml**: Incorrect. Metadata file (chart name, version).
- ✅ **B) values.yaml**: **CORRECT!** `values.yaml` contains default configuration variables injected into template files during rendering.
- ❌ **C) templates/deployment.yaml**: Incorrect. Kubernetes YAML template.
- ❌ **D) Chart.lock**: Incorrect. Dependency lockfile.
</default>

---

### Q49. Which CNCF Graduated tool continuously monitors a Git repository and automatically reconciles Kubernetes cluster state to match Git?
- [ ] A) Jenkins
- [ ] B) ArgoCD
- [ ] C) Docker Compose
- [ ] D) Terraform

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Jenkins**: Incorrect. Traditional CI pipeline tool.
- ✅ **B) ArgoCD**: **CORRECT!** `ArgoCD` is a CNCF Graduated GitOps continuous delivery tool that automatically reconciles cluster state with Git.
- ❌ **C) Docker Compose**: Incorrect. Local multi-container tool.
- ❌ **D) Terraform**: Incorrect. Infrastructure provisioning tool.
</details>

---

### Q50. What command packages a Helm chart directory into a versioned `.tgz` archive for registry distribution?
- [ ] A) `helm build`
- [ ] B) `helm package`
- [ ] C) `helm push`
- [ ] D) `helm create`

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) helm build**: Incorrect. Non-existent command.
- ✅ **B) helm package**: **CORRECT!** `helm package <chart-dir>` packages a chart into a versioned `.tgz` archive.
- ❌ **C) helm push**: Incorrect. Uploads a packaged chart to OCI registry.
- ❌ **D) helm create**: Incorrect. Scaffolds a new chart directory.
</details>
