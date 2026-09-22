# 🚦 Services & Ingress Networking (20% CKA Weight)

> **Exam Focus**: Expose workloads using ClusterIP, NodePort, and LoadBalancer Services, configure Ingress controllers, and write host/path-based Ingress routing rules.

---

## 1. Services (ClusterIP, NodePort, LoadBalancer)

### Concept
Services route traffic to Pods matching selector labels. ClusterIP exposes internally, NodePort opens host ports (30000-32767), and LoadBalancer interfaces with cloud load balancers.

### Generator Command
```bash
# Imperative creation of ClusterIP Service
kubectl create service clusterip web-svc --tcp=80:80 $do > svc-clusterip.yaml

# Imperative creation of NodePort Service
kubectl create service nodeport web-np --tcp=80:80 --nodeport=30080 $do > svc-nodeport.yaml

# Imperatively expose deployment as service
kubectl expose deployment nginx-deploy --name=nginx-svc --type=NodePort --port=80 $do > svc-expose.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-svc
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
```

### Verification/Debugging Command
```bash
# Verify service, endpoints, and connectivity
kubectl get svc web-svc
kubectl get endpoints web-svc
kubectl describe svc web-svc
```

---

## 2. Ingress Controller & Routing Rules

### Concept
Ingress manages external HTTP/HTTPS access to services, implementing host-based virtual hosting and path-based routing.

### Generator Command
```bash
# Imperative creation of Ingress resource with routing rules
kubectl create ingress app-ingress --rule="app.example.com/api*=api-service:8080" --rule="app.example.com/*=web-service:80" $do > ingress.yaml
```

### YAML Spec Snippet
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: app.example.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 8080
      - path: /
        pathType: Prefix
        backend:
          service:
            name: web-service
            port:
              number: 80
```

### Verification/Debugging Command
```bash
# Inspect Ingress status and assigned ingress IP/hostname
kubectl get ingress app-ingress
kubectl describe ingress app-ingress
curl -H "Host: app.example.com" http://<ingress-ip>/api
```
