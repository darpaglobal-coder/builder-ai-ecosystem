# ORIN open-source analytics component register

**Status:** evaluation shortlist only. Nothing in this list is installed or running by virtue of this document.

| Function | Candidate | Project / license review |
|---|---|---|
| Instrumentation standard | OpenTelemetry | Apache-2.0; vendor-neutral APIs, SDKs and collectors |
| Metrics | Prometheus | Apache-2.0; scrape and alert rule ecosystem |
| Dashboards | Grafana OSS | AGPL-3.0; review obligations and any enterprise-only features |
| Log aggregation | Grafana Loki | AGPL-3.0; review distribution/hosting obligations |
| Tracing | Jaeger | Apache-2.0; distributed tracing |
| Product analytics | Matomo | GPL-3.0; verify plugins, hosted vs self-hosted terms |
| Product analytics / feature flags | PostHog | MIT core plus separately licensed components; verify each module's current license |
| Error monitoring | GlitchTip | Open-source project; verify current license and compatibility |

## Selection criteria

- Current license and commercial-use obligations for each exact version/component.
- Security maintenance, release cadence, CVE response and dependency health.
- Tenant isolation, RBAC, SSO, audit events and encryption.
- Data residency, retention, deletion, export and backup/restore.
- Cardinality, ingestion throughput, query cost, storage and egress.
- API/webhook support, OpenTelemetry compatibility and portability.
- Operational complexity, on-call ownership and disaster recovery.

## Recommended logical pipeline

Application / authorized agent -> OpenTelemetry SDK -> Collector -> metrics backend (Prometheus), log backend (Loki), trace backend (Tempo or Jaeger) -> dashboards/alerts (Grafana).

Product analytics should be a separate, consent-gated pipeline. Do not route full application logs or sensitive traces into product analytics. Apply redaction and sampling at source and collector. Keep tenant identifiers scoped and avoid high-cardinality labels.

## License and supply-chain controls

Before adoption, pin a version and image digest, capture the SPDX license in an SBOM, review transitive dependencies, scan images, configure signed releases where available, and record any commercial/hosted service contract. Recheck licenses before upgrades. Do not claim an entire platform is “open source” when it bundles proprietary features or separately licensed modules.

## Deployment prerequisites

- Approved hosting account/project and budget.
- Persistent storage and tested backup/restore.
- Secret manager and TLS.
- Authentication, RBAC and tenant boundaries.
- Retention and deletion policies.
- Ingestion limits, quotas and cost alerts.
- Monitoring of the monitoring stack.
- Incident owner and on-call escalation.
- Production approval after preview tests.

## Baseline

Installed components verified: 0. Active telemetry backends verified: 0. This register does not deploy software or create external accounts.