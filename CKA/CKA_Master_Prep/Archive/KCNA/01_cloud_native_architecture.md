# ☁️ Cloud Native Architecture & CNCF Ecosystem (KCNA Domain - 16%)

## 1. What is Cloud Native?
Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds.

### Key Pillars of Cloud Native Architecture:
1. **Containers**: Package code with all dependencies for consistent execution across environments.
2. **Microservices**: Decompose monolithic applications into small, independently deployable services.
3. **Dynamic Orchestration**: Automated scheduling, scaling, and self-healing (Kubernetes).
4. **Declarative APIs**: Defining *desired state* in code rather than imperative script steps.
5. **Immutable Infrastructure**: Servers/containers are replaced rather than modified in place.

---

## 2. Monolithic vs. Microservices vs. Serverless

| Feature | Monolith | Microservices | Serverless / FaaS |
|---|---|---|---|
| **Deployment** | Single large binary/artifact | Multiple small independent services | Event-driven functions (e.g. OpenFaaS) |
| **Scaling** | Scale entire app together | Scale individual services independently | Scale down to 0 automatically |
| **Coupling** | Tightly coupled | Loosely coupled via APIs / gRPC | Event-driven / stateless |
| **State** | Stateful | Can be stateless/stateful | Strictly stateless |

---

## 3. The 12-Factor App Methodology (Cloud Native Best Practices)
1. **Codebase**: One codebase tracked in revision control, many deploys.
2. **Dependencies**: Explicitly declare and isolate dependencies.
3. **Config**: Store configuration in the environment (ConfigMaps/Secrets).
4. **Backing services**: Treat backing services (DBs, queues) as attached resources.
5. **Build, release, run**: Strictly separate build and run stages.
6. **Processes**: Execute the app as one or more stateless processes.
7. **Port binding**: Export services via port binding.
8. **Concurrency**: Scale out via the process model.
9. **Disposability**: Maximize robustness with fast startup and graceful shutdown.
10. **Dev/prod parity**: Keep development, staging, and production as similar as possible.
11. **Logs**: Treat logs as event streams.
12. **Admin processes**: Run admin/management tasks as one-off processes.

---

## 4. Service Mesh Architecture
A dedicated infrastructure layer for handling service-to-service communication, observability, and security without modifying application code.

- **Data Plane**: Sidecar proxies (Envoy) deployed alongside applications to intercept and route network traffic.
- **Control Plane**: Manages and configures proxies to enforce TLS encryption, traffic splitting, and telemetry.
- **Popular CNCF Service Meshes**: Istio, Linkerd, Consul.

---

## 5. CNCF Project Maturity Levels
CNCF hosts projects under 3 maturity stages:
1. **Sandbox**: Experimental early-stage projects (e.g., KubeArmor).
2. **Incubating**: Production-ready, growing adoption (e.g., KEDA, Longhorn).
3. **Graduated**: Highest maturity, broad enterprise adoption, rigorous governance (e.g., Kubernetes, Prometheus, Envoy, Helm, containerd, ArgoCD).
