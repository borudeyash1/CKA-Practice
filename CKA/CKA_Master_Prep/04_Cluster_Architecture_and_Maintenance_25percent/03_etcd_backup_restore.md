# 💾 ETCD Backup and Restore (25% CKA Weight - High Priority!)

> **Exam Focus**: Locate ETCD TLS certificates inside `/etc/kubernetes/pki/etcd/`, take an ETCD snapshot backup using `etcdctl`, and restore snapshot data to a custom directory, reconfiguring the ETCD static pod manifest.

---

## 1. Taking ETCD Snapshot Backup

### Concept
ETCD stores all Kubernetes cluster state data. Snapshots require authentication certificates (`--cacert`, `--cert`, `--key`) and `--endpoints`.

### Generator Command
```bash
# Save ETCD snapshot to file /var/lib/etcd-backup.db
ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /var/lib/etcd-backup.db
```

### YAML Spec Snippet
*N/A (etcdctl CLI Snapshot)*

### Verification/Debugging Command
```bash
# Verify snapshot status, hash, and file size
ETCDCTL_API=3 etcdctl --write-out=table snapshot status /var/lib/etcd-backup.db
```

---

## 2. Restoring ETCD Snapshot

### Concept
Restoring an ETCD snapshot writes cluster data to a new host directory (e.g. `/var/lib/etcd-restored`), after which the static pod manifest (`/etc/kubernetes/manifests/etcd.yaml`) must be updated to point hostPath volumes to the restored directory.

### Generator Command
```bash
# Restore snapshot to target directory
ETCDCTL_API=3 etcdctl \
  --data-dir=/var/lib/etcd-restored \
  snapshot restore /var/lib/etcd-backup.db
```

### YAML Spec Snippet
```yaml
# Edit volume hostPath inside /etc/kubernetes/manifests/etcd.yaml
apiVersion: v1
kind: Pod
metadata:
  name: etcd
  namespace: kube-system
spec:
  volumes:
  - name: etcd-data
    hostPath:
      path: /var/lib/etcd-restored
      type: DirectoryOrCreate
```

### Verification/Debugging Command
```bash
# Monitor static pod restart and verify restored resource presence
sudo crictl ps | grep etcd
kubectl get pods -A
```
