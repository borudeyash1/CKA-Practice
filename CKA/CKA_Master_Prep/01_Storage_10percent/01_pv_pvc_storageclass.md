# 💾 Storage: PV, PVC, StorageClass & Volume Mounts (10% CKA Weight)

> **Exam Focus**: PersistentVolumes (PV) supply cluster storage decoupled from Pod lifecycle, PersistentVolumeClaims (PVC) request volume size & access modes, and StorageClasses enable dynamic volume provisioning.

---

## 1. PersistentVolume (PV)

### Concept
PersistentVolume (PV) is a cluster-wide storage resource provisioned statically by an admin or dynamically using StorageClasses.

### Generator Command
```bash
# PVs cannot be generated imperatively via kubectl create; use dry-run template redirection
cat <<EOF > pv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  hostPath:
    path: "/mnt/data"
EOF
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  hostPath:
    path: "/mnt/data"
```

### Verification/Debugging Command
```bash
# Check PV status and details
kubectl get pv pv-analytics
kubectl describe pv pv-analytics
```

---

## 2. PersistentVolumeClaim (PVC)

### Concept
PersistentVolumeClaims (PVC) are namespace-scoped requests for storage that bind automatically to matching PVs based on size, access mode, and storageClassName.

### Generator Command
```bash
# Generates PVC manifest
cat <<EOF > pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-analytics
  namespace: default
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
  storageClassName: manual
EOF
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-analytics
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
  storageClassName: manual
```

### Verification/Debugging Command
```bash
# Check PVC binding status (Bound vs Pending)
kubectl get pvc pvc-analytics
kubectl describe pvc pvc-analytics
```

---

## 3. StorageClass & Dynamic Provisioning

### Concept
StorageClasses define the provisioner (e.g. `k8s.io/minikube-hostpath`, `ebs.csi.aws.com`) and parameters used to dynamically allocate storage when a PVC is created.

### Generator Command
```bash
# Generate StorageClass manifest
cat <<EOF > storageclass.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: k8s.io/minikube-hostpath
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: Immediate
EOF
```

### YAML Spec Snippet
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: k8s.io/minikube-hostpath
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: Immediate
```

### Verification/Debugging Command
```bash
# List cluster StorageClasses and check default annotation
kubectl get sc
kubectl describe sc fast-storage
```

---

## 4. Mounting PVC to Pod Spec

### Concept
Pods consume persistent storage by declaring a volume referencing the PVC name and specifying `volumeMounts` within the container definition.

### Generator Command
```bash
# Generate Pod with volume mount template
kubectl run storage-pod --image=nginx --port=80 $do > pod-storage.yaml
# Add volume and volumeMounts to generated pod-storage.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: storage-pod
spec:
  volumes:
  - name: data-volume
    persistentVolumeClaim:
      claimName: pvc-analytics
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: data-volume
```

### Verification/Debugging Command
```bash
# Verify volume mount inside container
kubectl exec -it storage-pod -- df -h /usr/share/nginx/html
kubectl describe pod storage-pod | grep -A 5 Volumes
```
