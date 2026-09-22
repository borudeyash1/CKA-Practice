# 🔑 RBAC: Roles, ClusterRoles & Bindings (25% CKA Weight)

> **Exam Focus**: Configure Role-Based Access Control (RBAC) to restrict user and ServiceAccount API access using Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings. Test access with `kubectl auth can-i`.

---

## 1. Roles & RoleBindings (Namespace-Scoped)

### Concept
Roles define API permissions (verbs: `get`, `list`, `create`, `delete`) on resources within a single namespace. RoleBindings grant those permissions to a User, Group, or ServiceAccount.

### Generator Command
```bash
# Imperative creation of Role in namespace 'dev'
kubectl create role pod-reader --verb=get,list,watch --resource=pods -n dev $do > role.yaml

# Imperative creation of RoleBinding linking Role to user 'john'
kubectl create rolebinding read-pods --role=pod-reader --user=john -n dev $do > rolebinding.yaml

# Imperative creation of ServiceAccount
kubectl create serviceaccount app-sa -n dev
```

### YAML Spec Snippet
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: dev
subjects:
- kind: User
  name: john
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

### Verification/Debugging Command
```bash
# Test permissions imperatively using auth can-i
kubectl auth can-i get pods --as=john -n dev
kubectl auth can-i delete deployments --as=john -n dev
kubectl auth can-i list pods --as=system:serviceaccount:dev:app-sa -n dev
```

---

## 2. ClusterRoles & ClusterRoleBindings (Cluster-Scoped)

### Concept
ClusterRoles define permissions across non-namespaced resources (Nodes, PVs) or cluster-wide namespaced resources. ClusterRoleBindings grant permissions cluster-wide.

### Generator Command
```bash
# Imperative creation of ClusterRole
kubectl create clusterrole node-inspector --verb=get,list --resource=nodes $do > clusterrole.yaml

# Imperative creation of ClusterRoleBinding to ServiceAccount
kubectl create clusterrolebinding inspect-nodes --clusterrole=node-inspector --serviceaccount=default:monitoring-sa $do > clusterrolebinding.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-inspector
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: inspect-nodes
subjects:
- kind: ServiceAccount
  name: monitoring-sa
  namespace: default
roleRef:
  kind: ClusterRole
  name: node-inspector
  apiGroup: rbac.authorization.k8s.io
```

### Verification/Debugging Command
```bash
# Verify ClusterRole permissions
kubectl get clusterrole node-inspector -o yaml
kubectl auth can-i get nodes --as=system:serviceaccount:default:monitoring-sa
```
