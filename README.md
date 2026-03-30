# AEGIS
## Overview
Aegis is an automated observability-driven incident response system for distributed services.
It collects and analyzes monitoring signals such as metrics, logs, and events, detects abnormal situations, and performs predefined response actions to improve service stability and reduce incident handling time.

## Built With

### Core
* [![Go][Go.dev]][Go-url]
* [![Gin][Gin-gonic]][Gin-url]
* [![PostgreSQL][Postgres]][Postgres-url]

### Observability Integrations
* [![Prometheus][Prometheus.io]][Prometheus-url]
* [![Loki][Loki]][Loki-url]
* [![Grafana][Grafana.com]][Grafana-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Goals
* collect telemetry from distributed services
* correlate metrics, logs, and external events
* detect incidents and abnormal states
* support automated response actions
* store incident context and execution state
* provide operators with visibility into decisions and actions

### Core functionality
* receiving events from external systems
(Grafana alerts, CI/CD webhooks, manual triggers)
* querying observability data sources
(Prometheus/VictoriaMetrics for metrics, Loki for logs)
* incident evaluation and enrichment
(checking related metrics/logs, confirming symptoms)
* rule-based decision making
(mapping incident type to response scenario)
* automated response actions
(restart service, rollback deployment, run script, send notification)
* recovery validation
(check whether service recovered after action)
* incident state persistence
(store incident lifecycle and actions in PostgreSQL)
* audit trail and observability of the system itself
(logs of decisions, actions, results)

## MVP
* monolithic architecture
* rule-based decision logic
* predefined automated actions
* integration with selected telemetry sources only
* focus on incident response for service-level failures

### Scenario 1: Post-deployment degradation
* CI/CD sends deployment event
* Aegis checks service metrics and logs
* Aegis detects increased error rate or latency
* Aegis triggers rollback or restart
* Aegis verifies service recovery
* Aegis stores incident result

### Scenario 2: Alert-driven recovery
* Grafana sends alert webhook
* Aegis queries metrics/logs for confirmation
* Aegis selects response policy
* Aegis executes action
* Aegis validates recovery and records outcome

### High-level modules of the monolith
* API layer
receives alerts, webhooks, manual requests
* Incident Manager
creates and tracks incident lifecycle
* Telemetry Analyzer
queries metrics and logs, enriches incidents
* Decision Engine
applies rules and selects response strategy
* Action Executor
executes automated remediation actions
* Recovery Verifier
checks service state after action
* Persistence layer
stores incidents, rules, actions, results
* Notification/Audit module
sends notifications and stores audit trail

<!-- MARKDOWN LINKS & IMAGES -->
[Go.dev]: https://img.shields.io/badge/Go-1.22-blue?logo=go
[Go-url]: https://go.dev/

[Gin-gonic]: https://img.shields.io/badge/Gin-Framework-00ADD8?logo=go
[Gin-url]: https://gin-gonic.com/

[Postgres]: https://img.shields.io/badge/PostgreSQL-DB-336791?logo=postgresql
[Postgres-url]: https://www.postgresql.org/

[Prometheus.io]: https://img.shields.io/badge/Prometheus-monitoring-orange?logo=prometheus
[Prometheus-url]: https://prometheus.io/

[Loki]: https://img.shields.io/badge/Loki-logs-0A0A0A?logo=grafana
[Loki-url]: https://grafana.com/oss/loki/

[Grafana.com]: https://img.shields.io/badge/Grafana-visualization-F46800?logo=grafana
[Grafana-url]: https://grafana.com/