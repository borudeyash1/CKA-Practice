# 🔐 Kubernetes Cluster Component Security (KCSA Domain 2 - 22%)

## 1. API Server Security Pipeline

All HTTP requests to `kube-apiserver` pass through three distinct security phases:

```text
Request ---> [ 1. Authentication ] ---> [ 2. Authorization ] ---> [ 3. Admission Control ] ---> etcd
```

1. **Authentication (AuthN)**: Validates identity of user/service (X.509 client certificates, OIDC tokens, ServiceAccount JWTs).
2. **Authorization (AuthZ)**: Verifies permissions (RBAC, ABAC, Webhook).
3. **Admission Control**: Intercepts request to mutate or validate objects before storing in `etcd` (e.g. Pod Security Admission, OPA Gatekeeper, Kyverno).

---

## 2. ETCD Encryption at Rest

By default, secrets stored in `etcd` are saved unencrypted in plain base64 text.

- To secure secrets at rest, configure `EncryptionConfiguration` file passed to `kube-apiserver` with `--encryption-provider-config`:
  - **Secretbox / AES-GCM / AES-CBC**: Symmetric key encryption.
  - **KMS (Key Management Service)**: Integration with external cloud KMS (AWS KMS, HashiCorp Vault, GCP KMS).

---

## 3. Kubelet Hardening
- **Disable Anonymous Authentication**: Set `--anonymous-auth=false`
- **Enable Webhook Authorization**: Set `--authorization-mode=Webhook`
- **Restrict Read-Only Port**: Disable unauthenticated read-only port `10255`.
- **Protect Node X.509 Certificates**: Enforce NodeRestriction admission plugin.
