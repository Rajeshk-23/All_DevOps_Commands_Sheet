# Prometheus & Grafana Cheatsheet

> Prometheus collects time-series metrics, while Grafana visualizes and alerts on operational data.

## Table of Contents
- [Prometheus PromQL Basics](#prometheus-promql-basics)
- [Prometheus Aggregation Operators](#prometheus-aggregation-operators)
- [Prometheus Functions](#prometheus-functions)
- [Prometheus Configuration & Operations](#prometheus-configuration--operations)
- [Prometheus promtool](#prometheus-promtool)
- [Grafana CLI](#grafana-cli)
- [Grafana HTTP API](#grafana-http-api)
- [Grafana Dashboards & Datasources](#grafana-dashboards--datasources)

## Prometheus PromQL Basics

| Command / Query | Description |
| --- | --- |
| `up` | Returns scrape health for all targets. |
| `up{job="api"}` | Filters a metric by an exact label match. |
| `up{instance=~"web-.*"}` | Filters labels with a regular expression. |
| `up{environment!="prod"}` | Excludes series with an exact label value. |
| `http_requests_total[5m]` | Selects a five-minute range vector. |
| `http_requests_total offset 1h` | Evaluates a selector one hour in the past. |
| `http_requests_total @ 1700000000` | Evaluates a selector at a Unix timestamp. |
| `vector(1)` | Creates an instant vector containing one. |
| `time()` | Returns the current evaluation timestamp in seconds. |

## Prometheus Aggregation Operators

| Command / Query | Description |
| --- | --- |
| `sum(http_requests_total)` | Sums all matching time series. |
| `sum by (job) (http_requests_total)` | Sums series while retaining the `job` label. |
| `sum without (instance) (http_requests_total)` | Sums series after dropping the `instance` label. |
| `avg by (job) (process_resident_memory_bytes)` | Calculates average memory by job. |
| `min by (job) (up)` | Finds the lowest value in each job. |
| `max by (job) (up)` | Finds the highest value in each job. |
| `count by (job) (up)` | Counts series in each job. |
| `topk(5, rate(http_requests_total[5m]))` | Returns the five highest request-rate series. |
| `count_values("version", build_info)` | Counts occurrences of each sample value. |

## Prometheus Functions

| Command / Query | Description |
| --- | --- |
| `rate(http_requests_total[5m])` | Calculates the per-second counter rate over five minutes. |
| `irate(http_requests_total[5m])` | Calculates an instant per-second rate from the latest samples. |
| `increase(http_requests_total[1h])` | Calculates total counter increase over one hour. |
| `delta(node_temperature_celsius[10m])` | Calculates gauge change over ten minutes. |
| `avg_over_time(up[15m])` | Calculates the average sample value over time. |
| `max_over_time(container_memory_usage_bytes[1h])` | Returns the maximum value over one hour. |
| `predict_linear(node_filesystem_free_bytes[6h], 86400)` | Predicts free space one day ahead. |
| `histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))` | Estimates the 99th-percentile request duration. |
| `label_replace(up, "host", "$1", "instance", "([^:]+):.*")` | Creates or rewrites a label using a regex. |
| `absent(up{job="api"})` | Returns a series when no matching target exists. |

## Prometheus Configuration & Operations

| Command / Query | Description |
| --- | --- |
| `scrape_configs:` | Declares targets Prometheus should scrape. |
| `job_name: node` | Names a scrape job. |
| `static_configs:` | Defines static target groups. |
| `targets: ['node:9100']` | Lists endpoints for a static target group. |
| `relabel_configs:` | Rewrites or filters labels before scraping. |
| `rule_files:` | Lists recording and alerting rule files. |
| `alerting:` | Configures Alertmanager integration. |
| `curl -X POST http://localhost:9090/-/reload` | Reloads configuration when lifecycle is enabled. |
| `curl http://localhost:9090/-/healthy` | Checks Prometheus health. |
| `curl http://localhost:9090/api/v1/targets` | Lists discovered and active targets. |

## Prometheus promtool

| Command / Query | Description |
| --- | --- |
| `promtool check config prometheus.yml` | Validates Prometheus configuration syntax. |
| `promtool check rules rules/*.yml` | Validates recording and alerting rules. |
| `promtool test rules rules.test.yml` | Executes rule unit tests. |
| `promtool query instant http://localhost:9090 'up'` | Runs an instant query against a server. |
| `promtool query range --start=2025-01-01T00:00:00Z --end=2025-01-01T01:00:00Z --step=60s http://localhost:9090 'up'` | Runs a range query against a server. |
| `promtool tsdb analyze /var/lib/prometheus` | Analyzes a local TSDB for label-cardinality issues. |

## Grafana CLI

| Command / Query | Description |
| --- | --- |
| `grafana cli plugins list-remote` | Lists plugins available from the catalog. |
| `grafana cli plugins install grafana-piechart-panel` | Installs a plugin by ID. |
| `grafana cli plugins update-all` | Updates all installed plugins. |
| `grafana cli plugins ls` | Lists locally installed plugins. |
| `grafana cli admin reset-admin-password 'NewPassword'` | Resets the Grafana administrator password. |
| `grafana cli admin data-migration encrypt-datasource-passwords` | Encrypts existing datasource passwords. |

## Grafana HTTP API

| Command / Query | Description |
| --- | --- |
| `curl -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/health` | Checks Grafana API health with a service-account token. |
| `curl -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/search` | Searches dashboards and folders. |
| `curl -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/dashboards/uid/<uid>` | Retrieves a dashboard by UID. |
| `curl -X DELETE -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/dashboards/uid/<uid>` | Deletes a dashboard by UID. |
| `curl -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/datasources` | Lists configured data sources. |
| `curl -X DELETE -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/datasources/uid/<uid>` | Deletes a data source by UID. |
| `curl -H 'Authorization: Bearer $GRAFANA_TOKEN' http://localhost:3000/api/folders` | Lists folders visible to the token. |

## Grafana Dashboards & Datasources

| Command / Query | Description |
| --- | --- |
| `POST /api/dashboards/db` | Creates or updates a dashboard from JSON. |
| `POST /api/datasources` | Creates a datasource from JSON. |
| `GET /api/datasources/uid/<uid>` | Retrieves a datasource by UID. |
| `PUT /api/datasources/uid/<uid>` | Updates a datasource by UID. |
| `POST /api/folders` | Creates a dashboard folder. |
| `GET /api/alerts` | Lists alert rules available through the legacy alerting API. |
| `GET /api/v1/provisioning/contact-points` | Lists Grafana Alerting contact points. |
| `GET /api/v1/provisioning/alert-rules` | Lists Grafana-managed alert rules. |
| `datasource.uid` | Binds a panel target to a stable datasource UID. |
| `${__interval}` | Uses Grafana's calculated query interval in a panel. |
