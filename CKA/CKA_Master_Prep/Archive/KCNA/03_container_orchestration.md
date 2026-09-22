# 🔌 Container Orchestration, Runtimes & Interfaces (KCNA Domain - 22%)

## 1. OCI Standards (Open Container Initiative)
The OCI is an open governance structure formed to create open industry standards for container formats and runtimes.

- **OCI Image Specification**: Defines software package format (layers, manifest, config).
- **OCI Runtime Specification**: Defines how to run an unpacked container filesystem (e.g. `runc`).

---

## 2. Container Runtime Interface (CRI)
The CRI API allows Kubernetes `kubelet` to use different container runtimes without recompiling the cluster code.

```text
[ kubelet ]  <--- (gRPC over Unix Domain Socket) --->  [ CRI Runtime ]  --->  [ OCI runc ]
```

### High-Level vs. Low-Level Runtimes:
- **High-Level Runtimes** (Manage images, storage, networks, CRI API): `containerd`, `CRI-O`.
- **Low-Level Runtimes** (Spawn and run container processes according to OCI spec): `runc`, `crun`, `kata-containers` (microVM isolation).

---

## 3. Container Networking Interface (CNI)
The CNI specification handles network interface allocation, IP address assignment (IPAM), and route configuration when a container/pod is created or deleted.

### Popular CNI Plugins Comparison:

| CNI Plugin | Primary Features | Network Model | Policy Support |
|---|---|---|---|
| **Flannel** | Simple, lightweight, easy setup | VXLAN overlay | ❌ No NetworkPolicy support |
| **Calico** | High performance, enterprise security | BGP / IP-in-IP overlay or flat routing |  Full NetworkPolicy support |
| **Cilium** | eBPF-powered, ultra-fast, L3-L7 security | eBPF native (no iptables overhead) |  Advanced L3-L7 NetworkPolicies |
| **Weave Net** | Automatic mesh networking & encryption | VXLAN mesh |  Basic NetworkPolicy support |

---

## 4. Container Storage Interface (CSI)
CSI enables storage vendors (NetApp, AWS, GCP, Ceph) to write out-of-tree plugins for persistent storage provisioning.

### CSI Storage Lifecycle:
1. Admin creates `StorageClass` with CSI provisioner info.
2. User creates `PersistentVolumeClaim` (PVC) requesting 10GB storage.
3. CSI Controller Plugin intercepts PVC and calls storage API (e.g., AWS EBS `CreateVolume`).
4. CSI Node Plugin mounts the volume directly into the Pod path (`/var/lib/kubelet/pods/...`).

---

## 5. Container Security Basics
- **Rootless Containers**: Running container runtimes as non-root users to limit blast radius.
- **Image Scanning**: Scanning image layers for known CVE vulnerabilities (Trivy, Grype).
- **Read-Only Root Filesystem**: Preventing malicious modifications inside container filesystems.
