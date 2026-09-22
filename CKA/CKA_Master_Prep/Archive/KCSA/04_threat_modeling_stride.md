# 🥷 Kubernetes Threat Model & STRIDE Framework (KCSA Domain 4 - 16%)

## 1. The STRIDE Threat Modeling Framework

STRIDE is a threat modeling methodology developed by Microsoft to identify software vulnerabilities across six threat categories:

| Letter | Threat Category | Security Property Violated | Kubernetes Example / Threat Vector |
|---|---|---|---|
| **S** | **Spoofing** | Authenticity | Impersonating a ServiceAccount token or master node API client certificate. |
| **T** | **Tampering** | Integrity | Modifying container images in registry or tampering with `etcd` database data. |
| **R** | **Repudiation** | Non-repudiation | Performing malicious cluster modifications when API Audit Logging is disabled. |
| **I** | **Information Disclosure** | Confidentiality | Exposing plain base64 Secrets or unencrypted pod-to-pod network traffic. |
| **D** | **Denial of Service** | Availability | Exhausting node resources (CPU/RAM/FD) via unconstrained Pods without ResourceQuotas. |
| **E** | **Elevation of Privilege** | Authorization | Escaping a container via `--privileged` mode to gain root access on the host node. |

---

## 2. Container Escape & Attack Vectors

- **Host Path Mounts**: Mounting `/` or `/var/run/docker.sock` / `/run/containerd/containerd.sock` into a container allows full host takeover.
- **Privileged Containers (`privileged: true`)**: Grants container processes access to host kernel devices (`/dev`) and capability flags.
- **Supply Chain Attacks**: Compromising upstream base images or CI/CD pipelines to inject malicious backdoors before deployment.
