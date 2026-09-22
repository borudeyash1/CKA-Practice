# 📋 Compliance, CIS Benchmarks & Audit Logging (KCSA Domain 6 - 10%)

## 1. CIS Kubernetes Benchmark & `kube-bench`

The Center for Internet Security (CIS) produces prescriptively hardened configuration benchmarks for Kubernetes control plane and worker nodes.

- **`kube-bench`**: Go application that checks whether Kubernetes is deployed securely according to CIS benchmarks.
```bash
# Run kube-bench on master node
kube-bench run --targets master
```

---

## 2. Kubernetes Audit Logging

Audit logs record the chronological sequence of actions in a cluster (Who did What, When, and How).

### Audit Levels:
1. `None`: Do not log events matching this rule.
2. `Metadata`: Log request metadata (requesting user, timestamp, resource, namespace), but not request/response body.
3. `Request`: Log request metadata and request body.
4. `RequestResponse`: Log request metadata, request body, and response body.

### Audit Policy Configuration (`audit-policy.yaml`):
```yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
  # Log Secret changes at Metadata level
  - level: Metadata
    resources:
    - group: ""
      resources: ["secrets"]
```
