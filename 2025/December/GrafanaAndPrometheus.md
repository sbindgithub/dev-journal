
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

Databases Grafana can connect to directly
✅ SQL databases (very common)

| Database             | Supported  |
| -------------------- | ---------- |
| MySQL                | ✅          |
| PostgreSQL           | ✅          |
| Microsoft SQL Server | ✅          |
| Oracle               | ✅ (plugin) |
| SQLite               | ✅ (plugin) |


Example use cases:

Business reports
Application data
Aggregated metrics stored in tables

| DB                         | Use case       |
| -------------------------- | -------------- |
| InfluxDB                   | Time-series    |
| Elasticsearch / OpenSearch | Logs & metrics |
| MongoDB                    | Document data  |
| ClickHouse                 | Analytics      |
| Azure Data Explorer        | Telemetry      |

✅ Cloud-managed databases

Grafana also connects to:

AWS RDS
Azure SQL
Google BigQuery
(Still just databases — cloud is optional)

# How this compares to Prometheus

| Aspect          | Prometheus                  | Database              |
| --------------- | --------------------------- | --------------------- |
| Data type       | Metrics (numbers over time) | Rows & columns        |
| Data collection | Pulls metrics               | You insert data       |
| Best for        | Monitoring                  | Reporting / analytics |
| Schema          | Label-based                 | Table-based           |

# When should you use DB instead of Prometheus?

✅ Use database when:

Data already exists in DB
Business / reporting dashboards
Low-frequency updates

✅ Use Prometheus when:

System metrics (CPU, memory)
High-frequency metrics
Alerts & monitoring

# Very common real-world setup

App metrics → Prometheus → Grafana
Business data → SQL DB → Grafana
Logs → Elasticsearch → Grafana

# Final takeaway

- Grafana is data-source agnostic.
- Prometheus is optional, not mandatory.

You can:

Use only SQL
Use only Prometheus
Use both together

# What Grafana actually does

Grafana:

Does not scrape metrics
Does not store Prometheus data
Does not run Prometheus internally

Grafana only:
Connects to Prometheus via HTTP
Uses PromQL to query it

# Where Prometheus runs

Prometheus runs:

- As a separate service on a VM
- In Docker
- In Kubernetes
- On-prem or cloud

Prometheus → http://localhost:9090
Grafana    → http://localhost:3000

| Question                             | Answer |
| ------------------------------------ | ------ |
| Is Prometheus built into Grafana?    | ❌ No   |
| Does Grafana install Prometheus?     | ❌ No   |
| Can Grafana work without Prometheus? | ✅ Yes  |
| Does Prometheus need Grafana?        | ❌ No   |

# Final takeaway

- Prometheus is external
- Grafana connects to it
- They are independent tools
- Often used together, but not bundled

# Prometheus is a time-series database (TSDB).

That means it stores:

- numbers
- over time
- with timestamps + labels

#example:

metric: cpu_usage_percent
labels: host=server1, core=0
time:   10:01:15
value:  72.5

# Prometheus DB vs traditional DB

| Feature        | Prometheus            | SQL DB          |
| -------------- | --------------------- | --------------- |
| Type           | Time-series DB        | Relational DB   |
| Data model     | Metrics + labels      | Tables + rows   |
| Query language | PromQL                | SQL             |
| Writes         | Append-only           | Insert / Update |
| Deletes        | Automatic (retention) | Manual          |
| Joins          | ❌ No                  | ✅ Yes           |
| Best for       | Monitoring            | Business data   |

# Prometheus is NOT a general-purpose database

You should NOT use Prometheus for:

- User data
- Orders
- Transactions
- Reports requiring joins

Prometheus is optimized only for:

- Metrics
- Monitoring
- Alerting

# Where data is stored

Prometheus stores data:

- Locally on disk
- In blocks
- With automatic retention (e.g., 15 days)

It does not depend on:

- MySQL
- PostgreSQL
- Any external DB

Metrics → Prometheus (TSDB) → Grafana
Business data → SQL DB → Grafana

# Prometheus is designed for:

- Numbers over time
- Aggregation
- Monitoring

❌ It is NOT designed for:

- Names
- Records
- Updates
- Joins
- CRUD operations

❌ Why “store in DB → pull into Prometheus” is wrong

Prometheus:

Scrapes metrics, not rows
Expects /metrics endpoint
Does not query SQL tables
Does not transform relational data

Trying to push employee rows into Prometheus would be:

Hard to model
Inefficient
Misuse of the tool
This is a design anti-pattern.

✅ Correct and industry-standard approach

✔️ Store employee data in a relational DB

Example:

SQL Server
PostgreSQL
MySQL
Oracle

✔️ Visualize employee data directly in Grafana

Grafana can connect directly to SQL DBs.

SQL DB ─────────▶ Grafana
Prometheus ─────▶ Grafana

Grafana sits on top and shows both kinds of data.

Example: Employee dashboard in Grafana (SQL)

```
SELECT
  department,
  COUNT(*) AS employee_count
FROM Employees
GROUP BY department;
```
Grafana shows:

Table

Bar chart

Pie chart

👉 No Prometheus involved.

# When Prometheus can be used (limited case)

You may expose aggregated metrics, not raw data.

```
employee_count{department="IT"} 42
employee_count{department="HR"} 15

```
This is OK because:

No personal data
Just numbers
Monitoring-friendly
But Prometheus is NOT the source of truth.

🧠 Golden rule (remember this forever)
Business data → Relational DB
Metrics data → Prometheus
Dashboards → Grafana

Employee DB ─────────▶ Grafana
System Metrics ──────▶ Prometheus ─▶ Grafana

# What gets stored in Prometheus?

Prometheus stores this result as time-series data:

```
employee_count{department="IT"} 42   @10:00
employee_count{department="HR"} 15   @10:00
```
What is NOT stored in Prometheus?

❌ SQL query
❌ C# code
❌ Aggregation logic
❌ Business rules

Prometheus has no idea:

where the number came from
how it was calculated
what table it used

# Where does the aggregation logic live then?

Outside Prometheus, always

Usually in:

Your application code
A custom exporter
A database exporter configuration

Relational DB
   ↓  (aggregation logic lives here)
Application / Exporter
   ↓  (only numbers exposed)
Prometheus

✅ This IS what Prometheus does

Receive already-aggregated numbers
Store them as time-series
Aggregate AGAIN over time if needed

# Two types of aggregation (don’t confuse them)

1️⃣ Business aggregation (BEFORE Prometheus)

COUNT employees
AVG salary
SUM orders

📍 Happens in DB / code

2️⃣ Time-series aggregation (INSIDE Prometheus)

rate()
avg_over_time()
sum by (label)
📍 Happens in PromQL

# Why this design exists

Prometheus is optimized for:

High write volume
Simple numeric values
Time-based queries

Storing logic would:

Break scalability
Break performance
Break simplicity

Prometheus stores “what the number was at that time”,
not “how the number was calculated”.

# Aggregate → Prometheus → Grafana

Relational DB
   ↓ (aggregation logic in code/exporter)
Prometheus (TSDB)
   ↓
Grafana

Use this when:

Monitoring trends over time
Alerting (thresholds, anomalies)
Frequent updates (every 15s, 30s, 1m)
System/operational metrics

Pros

**✔ Time-series history
✔ Alerting
✔ Efficient for monitoring**

Cons

❌ Not for detailed business data
❌ Extra setup

🧠 The key decision rule (remember this)

If the question is “what is the current state?” → Grafana + DB
If the question is “how does it change over time?” → Prometheus

🎯 Real-world example (very realistic)
Employee dashboard

| Metric                          | Path                             |
| ------------------------------- | -------------------------------- |
| Employee list                   | DB → Grafana                     |
| Employee count by dept          | DB → Grafana                     |
| Employee growth trend           | DB → code → Prometheus → Grafana |
| Alert: sudden drop in headcount | Prometheus                       |

🔄 Summary table

| Question           | Direct DB → Grafana | Prometheus → Grafana |
| ------------------ | ------------------- | -------------------- |
| Business reporting | ✅                   | ❌                    |
| Monitoring         | ❌                   | ✅                    |
| Alerting           | ❌                   | ✅                    |
| High frequency     | ❌                   | ✅                    |
| Historical trends  | ⚠️                  | ✅                    |



