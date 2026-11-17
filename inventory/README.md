# ORIN Global Asset, Application, Device and Network Inventory

**Status: design and schema only.** This change does not discover, enroll, scan, modify, or connect any external asset.

## Exact verified baseline

| Asset category | Verified count now | Evidence / interpretation |
|---|---:|---|
| GitHub repositories | 1 | `darpaglobal-coder/builder-ai-ecosystem` |
| Vercel projects | 1 | `orin-operations-console` |
| ORIN switchboard country workspaces | 195 | Static inventory entries; not separate apps |
| ORIN first-party web surfaces verified in repository | 1 | Static switchboard |
| Google OAuth clients active | 0 | No credentials/configuration verified |
| Apple Services IDs active | 0 | No credentials/configuration verified |
| Production identity brokers | 0 | None verified |
| Cloudflare accounts/zones/workers verified | 0 | Not connected in this session |
| Databases / durable queues / agent runtime verified | 0 | None verified in the current Vercel project inventory |
| User devices inventoried | 0 | No authorized device inventory source connected |
| AI agents verified as running | 0 | No running agent runtime verified |
| IPv4 endpoints inventoried | 0 | No authorized endpoint export supplied |
| IPv6 endpoints inventoried | 0 | No authorized endpoint export supplied |
| Chat-history export files imported | 0 | No ChatGPT export file supplied in this task |
| Beaconcha.in API credentials connected | 0 | No API key or account authorization supplied |
| POS / inventory connectors verified | 0 | No vendor credentials or connector evidence supplied |

These are verified counts from the accessible project context, not claims that the user owns no other devices, apps, services, or records.

## Capacity versus deployed inventory

The requested 100,000,000 applications/websites is a **capacity and catalog design target**, not an existing inventory and not 100 million deployments. The system must never fabricate records to meet a target. Store a 64-bit registry ID and paginate/shard by tenant and region. A row exists only after an owner-authorized discovery, import, or registration event with provenance.

A "possible integration" is not an active integration. Keep distinct lifecycle states: `proposed`, `discovered`, `owner_authorized`, `configured`, `tested`, `production_verified`, `suspended`, `retired`.

## Registry domains

1. Applications and websites: app ID, canonical URL, owner, environment, hosting, deployment, repo, domain, status, business purpose, privacy notice, data classification, auth audience, callback allowlist, contacts, evidence.
2. DNS and IP endpoints: domain, DNS provider, A/AAAA/CNAME records, IPv4/IPv6 address, prefix, port/service, environment, source, observation time, owner, authorization basis, expiry, exposure classification, TLS status, change history.
3. Devices: owner, device ID, manufacturer/model, OS/firmware, asset tag, enrollment source, management state, network interfaces, assigned user/role, security posture, last-seen time, consent/authorization record, removal workflow.
4. AI agents: agent ID, owner, purpose, runtime, model/provider, tools, service identity, allowed scopes, tenant boundary, budget/rate limits, data classification, human escalation, logs, heartbeat, version, evaluation results, kill switch.
5. Integrations: vendor, API product, owner account, scopes, credential reference (never secret value), contract/terms, rate limit, data flows, retention, cost, test evidence, renewal and revocation.
6. Chat history and files: source export ID, user-supplied archive, conversation ID, timestamps, attachment manifest, import consent, retention, deletion state, source provenance. Do not assume access to private ChatGPT history through this repository.
7. Revenue assets: offer/product, customer/tenant, pricing approval, contract, usage evidence, invoice/payment status, refund/chargeback state, direct costs, taxes, recognized revenue and reconciliation evidence.

## IPv4 / IPv6 handling

- Inventory only addresses from owner-authorized cloud, DNS, router, MDM, hosting, or network exports, or systems explicitly registered by the owner.
- Never scan arbitrary public address ranges, enumerate unrelated devices, or register third-party endpoints.
- Store IPv4 and IPv6 separately in canonical parsed form; preserve prefix length and source metadata.
- Treat dynamic addresses as time-bounded observations, not permanent ownership.
- Record private, loopback, link-local, ULA, public, and documentation ranges distinctly.
- IPv6 privacy extensions can rotate interface identifiers; do not use a changing address as a durable device identity.
- Do not infer physical location or individual identity from IP addresses.
- Keep endpoint exposure reports access-controlled and redact public IPs where publishing them would create risk.

## 24/7 ingestion and reporting target

Once deployed, ingestion workers should:
- accept signed webhooks and scheduled exports;
- deduplicate by source + immutable source ID;
- timestamp all observations in UTC;
- retain source, permission, scope, and collection purpose;
- quarantine malformed or unauthorized records;
- apply per-provider rate limits and backoff;
- emit immutable audit events;
- alert on expired credentials, unexpected endpoint changes, and stale inventory;
- reconcile source counts against imported counts;
- support export, correction, retention expiry, and deletion workflows.

A 24/7 target is not an operational claim until workers, persistent storage, alerting, on-call escalation, backups, and recovery are deployed and tested.

## Privacy report per app, device, agent and integration

Each report must show:
- data categories collected and why;
- data subjects and tenant scope;
- source and legal/contractual basis;
- purposes and downstream recipients;
- OAuth scopes and service permissions;
- data region and cross-border transfers;
- retention and deletion schedule;
- encryption and access-control posture;
- subprocessors and vendor terms;
- incident history and open risks;
- user rights and contact path;
- last review date, reviewer and evidence links.

Reports must be generated from observed configuration and evidence, not self-attested green statuses. Redact secrets, tokens, private keys, personal data and sensitive network details from reports.

## No hidden collection

No blanket access to all device data, all chat history, all Google services, or all company systems is implied. Each connector needs owner authorization and purpose-limited scopes. Users can revoke connections. No silent installation, background scraping, credential harvesting, permission escalation, or bypassing provider controls.
