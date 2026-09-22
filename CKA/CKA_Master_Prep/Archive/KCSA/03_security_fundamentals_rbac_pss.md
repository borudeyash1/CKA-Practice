# 🛡️ Kubernetes Security Fundamentals, RBAC & Pod Security Standards (KCSA Domain 3 - 22%)

## 1. Pod Security Standards (PSS) & Admission (PSA)

Kubernetes replaces legacy PodSecurityPolicy (PSP) with **Pod Security Standards**:

| PSS Profile | Description | Enforced Rules |
|---|---|---|
| **Privileged** | Unrestricted execution. | Known privilege escalations allowed. |
| **Baseline** | Prevents known privilege escalations with minimal restrictions. | Disallows host namespaces (`hostNetwork`, `hostPID`, `hostIPC`), hostPorts, elevated capabilities. |
| **Restricted** | Heavily restricted hardening. | Enforces non-root execution (`runAsNonRoot: true`), drops `ALL` capabilities, disallows privilege escalation, enforces read-only root FS. |

### Enforcing PSA via Namespace Labels:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: secure-apps
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/audit: restricted
    pod-security.kubernetes.io/warn: restricted
```

---

## 2. Secrets Management Best Practices
- Avoid exposing secrets in environment variables (visible in process lists `ps aux` and crash logs); prefer mounting Secrets as **volume files**.
- Use external secret managers (HashiCorp Vault, External Secrets Operator, AWS Secrets Manager).
