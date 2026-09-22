# ☸️ Certified Kubernetes Administrator (CKA) - 100% Exam Master Prep

Welcome to the consolidated **CKA Master Preparation Repository**. This repository is structured to prioritize official Linux Foundation **CKA Curriculum Domains**, emphasizing imperative speed, YAML generators, live troubleshooting, and hands-on cluster administration.

---

## 📊 CKA Curriculum Domain Weighting

| Domain | Weight | Repository Directory | Key Focus Topics |
| :--- | :---: | :--- | :--- |
| **Troubleshooting** | **30%** | [`/02_Troubleshooting_30percent`](file:///d:/Minikube/CKA/CKA_Master_Prep/02_Troubleshooting_30percent) | Application failures, Static Pods, Kubelet/Containerd, CoreDNS, CNI |
| **Cluster Architecture & Maintenance** | **25%** | [`/04_Cluster_Architecture_and_Maintenance_25percent`](file:///d:/Minikube/CKA/CKA_Master_Prep/04_Cluster_Architecture_and_Maintenance_25percent) | RBAC, Kubeadm Upgrades, ETCD Snapshot Backup/Restore, Node Drain |
| **Services & Networking** | **20%** | [`/05_Services_and_Networking_20percent`](file:///d:/Minikube/CKA/CKA_Master_Prep/05_Services_and_Networking_20percent) | ClusterIP, NodePort, Ingress, NetworkPolicies, CoreDNS |
| **Workloads & Scheduling** | **15%** | [`/03_Workloads_and_Scheduling_15percent`](file:///d:/Minikube/CKA/CKA_Master_Prep/03_Workloads_and_Scheduling_15percent) | Rolling Updates, ConfigMaps, Secrets, Probes, Taints/Tolerations |
| **Storage** | **10%** | [`/01_Storage_10percent`](file:///d:/Minikube/CKA/CKA_Master_Prep/01_Storage_10percent) | PV, PVC, StorageClass, Volume Mounts |
| **Imperative Speed Cheatsheet** | **N/A** | [`/00_Imperative_Commands_Cheatsheet`](file:///d:/Minikube/CKA/CKA_Master_Prep/00_Imperative_Commands_Cheatsheet) | Shortcuts, aliases, `--dry-run=client -o yaml` generators |

---

## 📁 CKA Master Prep Directory Structure

```text
CKA_Master_Prep/
├── 00_Imperative_Commands_Cheatsheet/
│   └── 01_imperative_kubectl_cheatsheet.md
├── 01_Storage_10percent/
│   └── 01_pv_pvc_storageclass.md
├── 02_Troubleshooting_30percent/
│   ├── 01_application_troubleshooting.md
│   ├── 02_controlplane_worker_troubleshooting.md
│   └── 03_network_troubleshooting.md
├── 03_Workloads_and_Scheduling_15percent/
│   ├── 01_pods_deployments_scaling.md
│   ├── 02_configmaps_secrets_securitycontext.md
│   ├── 03_multi_container_probes_jobs.md
│   └── 04_taints_tolerations_node_affinity.md
├── 04_Cluster_Architecture_and_Maintenance_25percent/
│   ├── 01_rbac_authentication.md
│   ├── 02_kubeadm_cluster_upgrade.md
│   ├── 03_etcd_backup_restore.md
│   └── 04_node_maintenance_ha.md
├── 05_Services_and_Networking_20percent/
│   ├── 01_services_and_ingress.md
│   ├── 02_network_policies.md
│   └── 03_coredns_cni.md
└── Archive/
    ├── KCNA/
    ├── KCSA/
    └── Minikube-Initialization/
```

---

## 📅 30-Day CKA Exam Preparation Progress Checklist

### ⚡ Phase 1: Speed & Imperative Generators (Days 1–3)
- [ ] **Day 1**: Master Shell Aliases (`k`, `do`, `now`) & bash autocompletion (`00_Imperative_Commands_Cheatsheet/01_imperative_kubectl_cheatsheet.md`)
- [ ] **Day 2**: Rapid Pod, Deployment, & Service YAML generation using `--dry-run=client -o yaml`
- [ ] **Day 3**: Fast ConfigMap, Secret, Job & CronJob generator shortcuts

### 🩺 Phase 2: Troubleshooting Masterclass (30% Weight) (Days 4–10)
- [ ] **Day 4**: Application failure states (`CrashLoopBackOff`, `ImagePullBackOff`, `Pending`) (`02_Troubleshooting_30percent/01_application_troubleshooting.md`)
- [ ] **Day 5**: Container log inspection (`kubectl logs --previous`) and shell execution (`kubectl exec`)
- [ ] **Day 6**: Memory resource limits & `OOMKilled` (Exit Code 137) container diagnosis
- [ ] **Day 7**: Control Plane Static Pod inspection (`/etc/kubernetes/manifests`, `crictl logs`) (`02_Troubleshooting_30percent/02_controlplane_worker_troubleshooting.md`)
- [ ] **Day 8**: Kubelet daemon & Containerd systemd service troubleshooting (`systemctl status`, `journalctl`)
- [ ] **Day 9**: CoreDNS resolution diagnostics & `kube-dns` service endpoints (`02_Troubleshooting_30percent/03_network_troubleshooting.md`)
- [ ] **Day 10**: CNI plugin daemonset readiness and host network interface validation

### 🔑 Phase 3: Cluster Architecture & Maintenance (25% Weight) (Days 11–18)
- [ ] **Day 11**: ServiceAccounts & API Authentication tokens (`04_Cluster_Architecture_and_Maintenance_25percent/01_rbac_authentication.md`)
- [ ] **Day 12**: Namespaced RBAC Roles & RoleBindings creation
- [ ] **Day 13**: Cluster-wide ClusterRoles & ClusterRoleBindings + testing permissions via `kubectl auth can-i`
- [ ] **Day 14**: Kubeadm Control Plane node upgrade process (`kubeadm upgrade plan/apply`) (`04_Cluster_Architecture_and_Maintenance_25percent/02_kubeadm_cluster_upgrade.md`)
- [ ] **Day 15**: Kubeadm Worker node upgrade process & Kubelet binary restart
- [ ] **Day 16**: ETCD snapshot backup (`etcdctl snapshot save` with TLS flags) (`04_Cluster_Architecture_and_Maintenance_25percent/03_etcd_backup_restore.md`)
- [ ] **Day 17**: ETCD snapshot restore (`etcdctl snapshot restore`) & static pod manifest volume update
- [ ] **Day 18**: Node Maintenance (`cordon`, `drain`, `uncordon`) & HA architecture (`04_Cluster_Architecture_and_Maintenance_25percent/04_node_maintenance_ha.md`)

### 🌐 Phase 4: Services & Networking (20% Weight) (Days 19–24)
- [ ] **Day 19**: Services (ClusterIP, NodePort, LoadBalancer) & TargetPort matching (`05_Services_and_Networking_20percent/01_services_and_ingress.md`)
- [ ] **Day 20**: Exposing Deployments imperatively (`kubectl expose`) & Endpoints inspection
- [ ] **Day 21**: Ingress Controller routing rules (Host-based and Path-based routing)
- [ ] **Day 22**: Ingress NetworkPolicies (Isolating inbound pod traffic) (`05_Services_and_Networking_20percent/02_network_policies.md`)
- [ ] **Day 23**: Egress NetworkPolicies (Restricting outbound CIDR/Namespace traffic)
- [ ] **Day 24**: CoreDNS `Corefile` ConfigMap customization & CNI plugin installation (`05_Services_and_Networking_20percent/03_coredns_cni.md`)

### 📦 Phase 5: Workloads & Scheduling (15% Weight) (Days 25–28)
- [ ] **Day 25**: Deployment Rolling Updates, Rollouts, and Revisions (`03_Workloads_and_Scheduling_15percent/01_pods_deployments_scaling.md`)
- [ ] **Day 26**: ConfigMaps, Secrets, & `securityContext` (runAsUser, readOnlyRootFilesystem) (`03_Workloads_and_Scheduling_15percent/02_configmaps_secrets_securitycontext.md`)
- [ ] **Day 27**: Multi-Container Pods (Sidecar pattern, shared emptyDir), Health Probes & Jobs (`03_Workloads_and_Scheduling_15percent/03_multi_container_probes_jobs.md`)
- [ ] **Day 28**: Taints & Tolerations (`NoSchedule`, `NoExecute`) & Node Affinity (`03_Workloads_and_Scheduling_15percent/04_taints_tolerations_node_affinity.md`)

### 💾 Phase 6: Storage & Final Practice (10% Weight) (Days 29–30)
- [ ] **Day 29**: PersistentVolumes (PV), PersistentVolumeClaims (PVC), StorageClasses & Pod Volume Mounts (`01_Storage_10percent/01_pv_pvc_storageclass.md`)
- [ ] **Day 30**: Full 2-Hour Time-Boxed CKA Practice Exam (killer.sh / simulator practice)

---

## 🗄️ Archive Reference

Theoretical and non-essential introductory materials have been safely moved to the [`/CKA_Master_Prep/Archive`](file:///d:/Minikube/CKA/CKA_Master_Prep/Archive) directory for reference:
- [`/Archive/KCNA`](file:///d:/Minikube/CKA/CKA_Master_Prep/Archive/KCNA) - Cloud Native Associate theory notes
- [`/Archive/KCSA`](file:///d:/Minikube/CKA/CKA_Master_Prep/Archive/KCSA) - Cloud Security Associate theory notes
- [`/Archive/Minikube-Initialization`](file:///d:/Minikube/CKA/CKA_Master_Prep/Archive/Minikube-Initialization) - Local cluster setup reference
