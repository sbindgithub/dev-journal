
# Prometheus collects & stores metrics. 
# Grafana visualizes them.

| Tool           | What it does                                                               |
| -------------- | -------------------------------------------------------------------------- |
| **Prometheus** | Pulls metrics from apps/servers, stores time-series data, evaluates alerts |
| **Grafana**    | Connects to Prometheus (and others) to build dashboards, charts, alerts    |

Think:

Prometheus = brain + memory

Grafana = eyes + UI

How data flows (step by step)

1️⃣ Your app exposes metrics
Example endpoint: /metrics

2️⃣ Prometheus scrapes metrics
Every N seconds, Prometheus pulls numbers like:

```http_requests_total{status="200"} 1245```

Application / Server
        ↓
   Prometheus (metrics + alerts)
        ↓
     Grafana (dashboards)

Alerts: who does what?

Prometheus

Evaluates alert rules (PromQL)

# Alertmanager

Sends alerts (email, Slack, PagerDuty)

Grafana

Can also show alerts visually (and trigger some alerts)

👉 In production, alerts are usually Prometheus + Alertmanager, dashboards in Grafana.

# Prometheus Query Language (PromQL)

It is a powerful, functional query language for selecting and aggregating time series data in the open-source monitoring system Prometheus. It is designed for building powerful queries for graphs, alerts, and recording rules. 

