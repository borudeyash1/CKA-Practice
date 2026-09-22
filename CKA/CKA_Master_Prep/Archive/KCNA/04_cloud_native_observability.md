# 📊 Cloud Native Observability & Application Delivery (KCNA Domain - 16%)

## 1. Observability Pillars & Prometheus Deep-Dive

Observability provides visibility into system internal state based on output telemetry.

### The 4 Metric Types in Prometheus:
1. **Counter**: Cumulative metric that only increases or resets to 0 on restart (e.g. total HTTP requests served: `http_requests_total`).
2. **Gauge**: Single numerical value that can arbitrarily go up or down (e.g. memory usage, CPU temperature, current active connections).
3. **Histogram**: Samples observations (usually things like request durations or response sizes) and counts them in configurable buckets (e.g. `http_request_duration_seconds_bucket`).
4. **Summary**: Similar to Histogram, calculates configurable quantiles (e.g. 50th, 90th, 99th percentiles) over a sliding time window.

### Prometheus Architecture:
- **Pull Model**: Prometheus server scrapes metrics targets over HTTP at configured intervals (`/metrics` endpoint).
- **Pushgateway**: Used for short-lived / batch jobs to push metrics before exiting.
- **Alertmanager**: Handles alerts sent by Prometheus, dedupes, groups, and routes to Slack/Email/PagerDuty.
- **PromQL (Prometheus Query Language)**:
  ```promql
  # Rate of HTTP requests over 5 minutes
  rate(http_requests_total[5m])
  ```

---

## 2. Distributed Tracing & Logging

- **Distributed Tracing**: Tracking a single request transaction through multiple microservice boundaries using a unique `Trace ID` and `Span ID`.
- **Tools**: OpenTelemetry, Jaeger, Zipkin.
- **Logging Aggregation**: Log shipping agents collect stdout/stderr streams from node log directories (`/var/log/containers`).
- **Tools**: Fluentd, Fluent Bit, Grafana Loki.

---

## 3. GitOps Principles (ArgoCD & Flux)

GitOps is an operational framework that applies DevOps best practices (version control, collaboration, compliance) to infrastructure automation.

### 4 Core GitOps Principles:
1. **Declarative**: The entire system is described declaratively.
2. **Version Controlled & Canonical**: Desired state is stored in Git.
3. **Automated Pull**: Approved changes are automatically pulled and applied to the cluster by software agents (ArgoCD / Flux).
4. **Continuous Reconciliation**: Software agents continuously monitor cluster state and fix configuration drift.

---

## 4. Helm Package Management

Helm is the official package manager for Kubernetes.

- **Chart**: A package containing all resource definitions needed to run an app.
- **Chart.yaml**: Metadata file describing the chart (version, name, description).
- **values.yaml**: Default configuration values for templates.
- **templates/**: Folder containing Kubernetes YAML template files parsed with Go templating engine.

### Essential Helm Commands:
```bash
# Add repo
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Install chart
helm install my-release bitnami/wordpress

# Upgrade release
helm upgrade my-release bitnami/wordpress --set service.type=NodePort

# List releases
helm list

# Uninstall release
helm uninstall my-release
```
