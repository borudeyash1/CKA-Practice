# 🛡️ The 4Cs of Cloud Native Security & Fundamentals (KCSA Domain 1 - 14%)

## 1. The 4Cs Security Model

Cloud Native Security is structured in 4 nested layers. Each layer builds upon the security of the layer beneath it. Securing inner layers cannot compensate for insecure outer layers!

```text
+-------------------------------------------------------+
|                       1. CLOUD                        |
|  +-------------------------------------------------+  |
|  |                   2. CLUSTER                    |  |
|  |  +-------------------------------------------+  |  |
|  |  |               3. CONTAINER                |  |  |
|  |  |  +-------------------------------------+  |  |  |
|  |  |  |               4. CODE               |  |  |  |
|  |  |  +-------------------------------------+  |  |  |
|  |  +-------------------------------------------+  |  |
|  +-------------------------------------------------+  |
+-------------------------------------------------------+
```

### The 4 Layers Breakdown:
1. **Cloud (Infrastructure)**: Physical datacenter security, VPC networking, cloud provider IAM, security groups, TLS endpoints.
2. **Cluster**: Kubernetes control plane API server, node authentication, RBAC, ETCD encryption at rest, NetworkPolicies, CNI plugins.
3. **Container**: Base OS image vulnerability scanning, rootless containers, restricted capabilities, read-only root filesystems, minimal base images (Distroless / Alpine).
4. **Code**: Application source code security, SAST scanning, dependency vulnerability management (Snyk/Trivy), TLS configuration, input sanitization.

---

## 2. Shift-Left Security & Defense in Depth

- **Shift-Left**: Integrating security automated checks earlier in the software development lifecycle (during code write and CI build phase rather than waiting for production deployment).
- **Defense in Depth**: Implementing redundant, overlapping security controls so that if one security layer fails (e.g., container escape), subsequent layers (e.g. AppArmor/seccomp/network policy) prevent compromise.
- **Shared Responsibility Model**: Cloud providers manage physical infrastructure security, while customers manage cluster configuration, network policies, IAM, and application security.
