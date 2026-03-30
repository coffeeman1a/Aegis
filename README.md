<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a id="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![project_license][license-shield]][license-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/coffeeman1a/Aegis">
    <img src="images/logo.svg" alt="Logo" width="120" height="120">
  </a>

<h3 align="center">Aegis</h3>

  <p align="center">
    Aegis is an automated observability-driven incident response system for distributed services.
It collects and analyzes monitoring signals such as metrics, logs, and events, detects abnormal situations, and performs predefined response actions to improve service stability and reduce incident handling time.
    <br />
    <a href="https://github.com/coffeeman1a/Aegis"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/coffeeman1a/Aegis">View Demo</a>
    &middot;
    <a href="https://github.com/coffeeman1a/Aegis/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/coffeeman1a/Aegis/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>


<!-- ABOUT THE PROJECT -->
## About The Project
### Built With

*Core*
* [![Go][Go.dev]][Go-url]
* [![Gin][Gin-gonic]][Gin-url]
* [![PostgreSQL][Postgres]][Postgres-url]

*Observability Integrations*
* [![Prometheus][Prometheus.io]][Prometheus-url]
* [![Loki][Loki]][Loki-url]
* [![Grafana][Grafana.com]][Grafana-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Goals

- Collect telemetry and events from distributed systems  
- Normalize and ingest events from heterogeneous sources  
- Correlate metrics, logs, and external events  
- Detect incidents and abnormal states  
- Support automated and consistent response actions  
- Store incident context and execution state  
- Provide operators with visibility into decisions and actions  

## Core Functionality

### Event Ingestion

- Receiving events from external systems:
  - Grafana Alerting (webhooks)
  - CI/CD pipelines
  - Manual/API triggers  
- Validation of incoming payloads  
- Normalization into a unified internal event format  
- Metadata enrichment:
  - `event_id`
  - `source`
  - `timestamp`
  - `event_type`  
- Publishing events to the message broker  

---

### Incident Processing

- Consuming events from broker  
- Querying observability data sources:
  - Prometheus / VictoriaMetrics (metrics)  
  - Loki (logs)  
- Incident evaluation and enrichment  
- Correlation with existing incidents  

---

### Decision and Response

- Rule-based decision engine  
- Mapping incident types to response strategies  
- Automated response actions:
  - Service restart  
  - Deployment rollback  
  - Script execution  
  - Notification dispatch  

---

### Recovery and State Management

- Recovery validation after action execution  
- Incident lifecycle management  
- Persistent storage of:
  - incidents  
  - actions  
  - execution results  
- Idempotent action execution  
- Deduplication of repeated events  

---

### Audit and Observability

- Audit trail of:
  - decisions  
  - actions  
  - outcomes  
- Internal logging and observability of the system  

---

### MVP

<br />
<div align="center">
  <a href="https://github.com/coffeeman1a/Aegis">
    <img src="images/schema.svg" alt="Schema">
  </a>
</div>

* event-driven architecture with asynchronous processing
* two main services:
  * Event Gateway (event ingestion and normalization)
  * Incident Orchestrator (analysis, decision-making, execution)
* message broker (NATS JetStream) for buffering and delivery
* rule-based decision logic
* predefined automated actions
* integration with selected telemetry sources only
* focus on incident response for service-level failures

### Scenario 1: Post-deployment degradation
* CI/CD sends deployment event to Event Gateway
* Event Gateway normalizes event and publishes it to broker
* Incident Orchestrator consumes event from broker
* Orchestrator queries service metrics and logs
* detects increased error rate or latency
* selects response strategy (rollback or restart)
* executes action
* verifies service recovery
* stores incident result

### Scenario 2: Alert-driven recovery
* Grafana sends alert webhook to Event Gateway
* Event Gateway normalizes event and publishes it to broker
* Incident Orchestrator consumes event from broker
* Orchestrator queries metrics/logs for confirmation
* correlates event with existing incidents (if any)
* selects response policy
* executes action
* validates recovery
* records outcome


<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/coffeeman1a/Aegis.svg?style=for-the-badge
[contributors-url]: https://github.com/coffeeman1a/Aegis/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/coffeeman1a/Aegis.svg?style=for-the-badge
[forks-url]: https://github.com/coffeeman1a/Aegis/network/members
[stars-shield]: https://img.shields.io/github/stars/coffeeman1a/Aegis.svg?style=for-the-badge
[stars-url]: https://github.com/coffeeman1a/Aegis/stargazers
[issues-shield]: https://img.shields.io/github/issues/coffeeman1a/Aegis.svg?style=for-the-badge
[issues-url]: https://github.com/coffeeman1a/Aegis/issues
[license-shield]: https://img.shields.io/github/license/coffeeman1a/Aegis.svg?style=for-the-badge
[license-url]: https://github.com/coffeeman1a/Aegis/blob/master/LICENSE.txt

<!-- Shields.io badges -->
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