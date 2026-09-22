# 🛠️ Platform Security: Trivy, Falco, OPA Gatekeeper & Supply Chain (KCSA Domain 5 - 16%)

## 1. Image Vulnerability Scanning (Trivy & Grype)

- **Trivy**: Comprehensive vulnerability scanner for container images, file systems, Git repositories, and Kubernetes manifests.
```bash
# Scan container image for CRITICAL vulnerabilities
trivy image --severity CRITICAL nginx:latest
```

---

## 2. Runtime Security & Anomaly Detection (Falco)

- **Falco**: CNCF Graduated runtime security tool that uses Linux eBPF kernel probes to detect anomalous behaviors in real time.
- **Example Falco Triggers**:
  - A shell is spawned inside a running production container (`exec /bin/sh`).
  - Sensitive file `/etc/shadow` is read by an unauthorized process.
  - Unexpected outbound network connection from a database pod.

---

## 3. Admission Control & Policy Engines (OPA / Gatekeeper & Kyverno)

- **OPA / Gatekeeper**: Validates and mutates Kubernetes resource requests using **Rego** declarative policy language.
- **Kyverno**: Kubernetes-native policy engine using YAML manifests (no custom Rego learning required).

---

## 4. Supply Chain Security & Image Signing (Cosign / Sigstore & SBOM)

- **Cosign (Sigstore)**: Signs and verifies container images using cryptographic keys or OIDC keyless signing.
- **Software Bill of Materials (SBOM)**: Nested inventory of software components and dependencies inside a container image (generated via Syft/Trivy).
