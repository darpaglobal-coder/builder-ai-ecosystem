# ORIN analytics, telemetry and observability

**Status: implementation blueprint; no analytics provider is connected or collecting data from this commit.** This design covers only assets the owner authorizes and systems that expose documented APIs, exports, webhooks or supported telemetry. It does not grant access to Google accounts, third-party sites, devices, networks or private datasets.

## Measurement domains

Use a common event envelope across first-party services:

- Product analytics: page/screen views, feature usage, navigation, conversion funnels and aggregate engagement.
- Application health: request count, latency percentiles, error rates, availability and saturation.
- Infrastructure: CPU, memory, disk, queue depth, worker heartbeat, deployment and resource utilization.
- Security: authentication outcomes, permission changes, privileged actions, suspicious events and incident timelines.
- Data pipelines: source freshness, records received/rejected/deduplicated, processing lag and reconciliation.
- Business operations: tenant usage, subscriptions, invoices, refunds, support response and unit economics.
- Integrations: API calls, rate-limit responses, webhook delivery, credential expiry state (never credential values), provider costs and sync health.
- AI agents: invocation count, tool calls, latency, token/cost budgets, policy denials, evaluation results, human handoffs and failure rates. Never log hidden reasoning or unrestricted prompt contents.

## Collection rules

1. **Default deny for optional analytics.** Essential security/operational logs are purpose-limited; optional product analytics and advertising tags remain disabled until the visitor's choice and applicable legal basis are recorded.
2. **Consent-first Google Analytics.** Do not load Google tags or send events until the configured consent mechanism records an affirmative analytics choice. Provide reject and withdraw controls with comparable ease. Keep analytics consent separate from advertising consent.
3. **No sensitive payloads.** Never send names, email addresses, phone numbers, precise location, authentication tokens, payment data, health data, private messages, raw IP addresses, or stable device identifiers to GA. Do not place personal data in URLs, event names, custom dimensions, or error messages.
4. **Pseudonymous IDs only when justified.** Rotate or scope identifiers by tenant and purpose; do not cross-stitch authenticated and anonymous sessions without valid consent and legal authorization.
5. **Minimize and aggregate.** Prefer counts, duration buckets, coarse region, service/version, and pseudonymous tenant-level usage over user-level trails.
6. **Document every source.** Every event has a source asset, owner, purpose, authorization reference, schema version, timestamp, and retention class.
7. **Respect revocation and deletion.** Stop future optional collection immediately; support provider-side deletion where available and maintain a deletion audit without retaining the deleted payload.
8. **No third-party surveillance.** No arbitrary crawling, network scanning, browser fingerprinting, hidden device enrollment, or collection from systems without owner authorization.

## Google Analytics 4 integration

Google Analytics is a **provider option**, not active by default. Activation requires:
- a Google Analytics property and web data stream owned/authorized by the operator;
- a Measurement ID stored as public configuration (not an API secret);
- a consent management implementation and reviewed privacy notice;
- an approved data map, retention setting, region configuration and event allowlist;
- testing that no Google tag/network request occurs before analytics consent;
- server-side Measurement Protocol secrets stored only in a managed secret store, never in client code, Git, logs or chat;
- an owner-approved deployment and post-deploy verification.

Use **basic consent mode** as the conservative default: block Google tags entirely until the user opts in. If a future legal/privacy review chooses advanced consent mode, document that denied-state cookieless pings may still be transmitted. Never silently switch modes. Do not activate advertising features, Google Signals, remarketing, user-provided data, or cross-device identity stitching as part of baseline analytics.

Event allowlist (initial proposal): `page_view`, `sign_up`, `login_success`, `feature_used`, `checkout_started`, `purchase_completed`, `subscription_changed`, `support_requested`. Event parameters must be allowlisted, short, non-sensitive and validated. Never send free-form text.

## Open-source observability options

Prefer open standards and self-hostable components where practical:

| Layer | Candidate | Purpose | Deployment caveat |
|---|---|---|---|
| Instrumentation | OpenTelemetry | Vendor-neutral traces, metrics and logs | SDKs/exporters still need configuration and sampling |
| Metrics | Prometheus | Time-series service and infrastructure metrics | Configure retention, cardinality limits and durable storage |
| Dashboards | Grafana | Dashboards and alert visualization | Secure admin access, tenant isolation and plugin review |
| Logs | Grafana Loki | Indexed log labels with log storage | Avoid high-cardinality labels and sensitive log content |
| Traces | Jaeger or Tempo | Distributed request traces | Sampling and retention required |
| Error tracking | GlitchTip or self-hosted Sentry-compatible option | Exceptions and releases | Verify license, edition features and data residency |
| Product analytics | Matomo or PostHog | First-party product usage | Verify current license, hosting terms, cookie behavior and commercial terms before selection |

These are candidate technologies, not installed or active services. Pin reviewed versions, scan dependencies, document licenses, maintain SBOMs, and budget hosting/storage/egress. Do not assume every feature of a project is open source under the same license.

## Reliability and alerting

- Use UTC timestamps and monotonic durations.
- Include trace IDs and request IDs; do not include secrets or direct identifiers.
- Set per-service SLOs only after measuring a baseline.
- Alert on availability, error budget burn, p95/p99 latency, queue lag, failed syncs, stale sources, exhausted budgets, credential expiry and backup failures.
- Use bounded-cardinality metric labels; never label metrics with email, user ID, full URL, IP or arbitrary user input.
- Define alert owner, severity, runbook, escalation window and acknowledgement.
- Test alert delivery and incident drills before claiming 24/7 coverage.
- Back up configuration and critical telemetry; test restore and retention deletion.
- Keep an immutable, access-controlled audit trail for admin and security events.

## Operational status definitions

`planned` = documented only; `configured` = credentials/config present; `connected` = provider handshake succeeded; `ingesting` = fresh events observed; `verified` = dashboard, alerts, consent and deletion tests passed; `paused` = collection disabled; `retired` = connector removed.

A provider must not be labelled active based on documentation, a saved API key, a successful deployment, or an HTTP 200 alone. Require fresh source timestamps and a successful end-to-end test.

## Current ORIN baseline

- Active GA properties / data streams verified: **0**
- GA Measurement IDs configured: **0**
- GA API secrets configured: **0**
- Consent manager deployed and verified: **0**
- Open-source telemetry backends verified: **0**
- Production log/metric/trace pipelines verified: **0**
- Alert routes and on-call coverage verified: **0**

These are the counts verified from the accessible project configuration, not claims that no other assets exist in external accounts.

## Activation checklist

1. Inventory each first-party domain/app and assign a data owner.
2. Approve the data map, legal basis, retention, privacy notice and consent UI.
3. Select the analytics/observability components and review licenses/security.
4. Provision owned accounts and secrets in provider consoles/secret manager.
5. Add per-environment configuration; keep preview and production IDs separate.
6. Implement the event allowlist and consent gate; add unit/integration tests.
7. Deploy to preview; verify network requests, redaction, rejection, withdrawal and deletion.
8. Obtain explicit production-release approval; deploy and verify fresh events, dashboards and alert routes.
9. Publish the privacy notice and maintain a dated change log.

## References

- Google Analytics developer setup: https://developers.google.com/analytics/devguides/collection/ga4
- Google Analytics Measurement Protocol: https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference
- Google Analytics Measurement Protocol policy: https://developers.google.com/analytics/devguides/collection/protocol/ga4/policy
- Google Consent Mode: https://developers.google.com/tag-platform/security/concepts/consent-mode
- OpenTelemetry: https://opentelemetry.io/docs/
- Prometheus: https://prometheus.io/docs/
- Grafana: https://grafana.com/docs/
- Matomo: https://matomo.org/
- PostHog: https://posthog.com/

This is engineering documentation, not legal advice. Have qualified counsel review the final implementation for each jurisdiction and product.