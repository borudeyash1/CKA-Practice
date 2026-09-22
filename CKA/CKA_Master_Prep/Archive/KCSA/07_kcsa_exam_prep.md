# 🎯 KCSA Interactive Practice Exam (Questions with ✅/❌ Validation)

Test your readiness for the KCSA Security exam! Click **Reveal Answer & Validation** under each question to check your answer with clear tick mark ✅ and cross mark ❌ explanations.

---

## Domain 1: Cloud Native Security

### Q1. In the 4Cs model of Cloud Native Security (Cloud, Cluster, Container, Code), which layer is considered the outermost foundational layer?
- [ ] A) Code
- [ ] B) Container
- [ ] C) Cluster
- [ ] D) Cloud

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Code**: Incorrect. Code is the innermost application layer.
- ❌ **B) Container**: Incorrect. Container is layer 3.
- ❌ **C) Cluster**: Incorrect. Cluster is layer 2.
- ✅ **D) Cloud**: **CORRECT!** In the nested 4Cs model (Cloud $\to$ Cluster $\to$ Container $\to$ Code), Cloud/Infrastructure is the outermost foundational layer.
</details>

---

### Q2. What does the "Shift-Left" security principle advocate?
- [ ] A) Moving container instances to the left rack in a physical datacenter.
- [ ] B) Integrating security automated checks earlier in the software development lifecycle (CI/CD build phase).
- [ ] C) Disabling root privileges on Linux worker nodes.
- [ ] D) Shifting cloud costs from production to staging environments.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Rack moving**: Incorrect. Irrelevant.
- ✅ **B) CI/CD Early Checks**: **CORRECT!** "Shift-Left" means embedding automated security vulnerability scans early in development and build stages.
- ❌ **C) Disabling root**: Incorrect. That is container hardening.
- ❌ **D) Shifting costs**: Incorrect. FinOps concept.
</details>

---

## Domain 2: Cluster Component Security

### Q6. Which phase of the `kube-apiserver` request processing pipeline evaluates whether a user has permission to create a Pod in a specific namespace?
- [ ] A) Authentication (AuthN)
- [ ] B) Authorization (AuthZ)
- [ ] C) Mutating Admission Control
- [ ] D) Validating Admission Control

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Authentication**: Incorrect. AuthN verifies *who* the caller is.
- ✅ **B) Authorization**: **CORRECT!** AuthZ (evaluating RBAC rules) determines *what* permissions the authenticated identity has.
- ❌ **C) Mutating Admission**: Incorrect. Modifies request payloads.
- ❌ **D) Validating Admission**: Incorrect. Validates custom business policies.
</details>

---

### Q7. How are secrets stored in `etcd` by default if no EncryptionConfiguration is specified?
- [ ] A) Encrypted with AES-256 symmetric keys.
- [ ] B) Encrypted via KMS.
- [ ] C) Unencrypted in plain Base64 text.
- [ ] D) Hashed using SHA-512.

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) AES-256**: Incorrect. Encryption must be manually configured via KMS or Secretbox provider.
- ❌ **B) KMS**: Incorrect. Requires external cloud integration.
- ✅ **C) Plain Base64**: **CORRECT!** By default, Kubernetes stores Secrets unencrypted in plain Base64 text inside `etcd`.
- ❌ **D) SHA-512**: Incorrect. Secrets must be readable by the control plane so hashing is not used.
</details>

---

## Domain 3: Security Fundamentals & PSS

### Q11. Under Kubernetes Pod Security Standards (PSS), which profile enforces non-root container execution (`runAsNonRoot: true`) and drops all Linux capabilities by default?
- [ ] A) Privileged
- [ ] B) Baseline
- [ ] C) Restricted
- [ ] D) HostAccess

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Privileged**: Incorrect. Allows full host privileges.
- ❌ **B) Baseline**: Incorrect. Prevents known escalations but allows default root execution.
- ✅ **C) Restricted**: **CORRECT!** The `Restricted` PSS profile enforces strict hardening, including non-root execution (`runAsNonRoot: true`) and dropping capabilities.
- ❌ **D) HostAccess**: Incorrect. Non-existent PSS profile.
</details>

---

## Domain 4: Threat Model & STRIDE

### Q15. In the STRIDE threat model, what does the letter 'E' stand for?
- [ ] A) Encryption
- [ ] B) Elevation of Privilege
- [ ] C) Eviction of Pods
- [ ] D) Error Logging

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Encryption**: Incorrect.
- ✅ **B) Elevation of Privilege**: **CORRECT!** In STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege), E stands for Elevation of Privilege.
- ❌ **C) Eviction of Pods**: Incorrect.
- ❌ **D) Error Logging**: Incorrect.
</details>

---

## Domain 5: Platform Security

### Q18. Which CNCF Graduated tool uses Linux eBPF kernel probes to detect real-time runtime security anomalies (such as an interactive shell execution inside a production container)?
- [ ] A) Trivy
- [ ] B) Falco
- [ ] C) Helm
- [ ] D) Prometheus

<details>
<summary><b>🔍 Reveal Answer & Validation</b></summary>

- ❌ **A) Trivy**: Incorrect. Trivy is a static vulnerability scanner.
- ✅ **B) Falco**: **CORRECT!** `Falco` leverages Linux eBPF probes for real-time runtime threat detection.
- ❌ **C) Helm**: Incorrect. Package manager.
- ❌ **D) Prometheus**: Incorrect. Metrics collection tool.
</details>
