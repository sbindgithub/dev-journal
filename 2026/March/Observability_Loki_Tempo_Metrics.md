## Search by corelation Id:
{k8s_cluster="nscm-prod-west-1", app="mcl-ob-lns-cs", env="prod"}
| json
| CorrelationId="1001081458"
| line_format "{{._timestamp}} | Trace={{.TraceId}} | Offset={{.Offset}} | {{.Message}}"


## Search by TraceId
{k8s_cluster="nscm-prod-west-1", app="mcl-ob-lns-cs", env="prod"}
| json
| TraceId="2d7f208dffe70fcfc2923e9b29314294"


## Grafana Loki

Purpose: Log aggregation system

Typical data stored:

Log line
Timestamp
Labels (app, pod, namespace, env)

Loki stores application logs and allows you to search them efficiently using labels.
Characteristics:

Designed for high-volume log storage
Uses label-based indexing
Stores raw log messages
Used to troubleshoot errors, warnings, or business events

## Grafana Tempo

Purpose: Distributed tracing storage
Tempo stores traces and spans, not logs.

Typical data stored:

TraceId
SpanId
ParentSpanId
ServiceName
Duration

## Metrics

Prometheus is used to collect and store metrics, which are numeric measurements about system behavior over time.
Metrics are different from logs and traces. They are time-series data.

Example metric:

timestamp        metric_name              value
10:00:01         http_requests_total      1520
10:00:02         http_requests_total      1525

Prometheus continuously collects these values and stores them as time series.

Metrics  → Prometheus → "Is the system healthy?"
Logs     → Loki       → "What exactly happened?"
Traces   → Tempo      → "Where did the request go?"
