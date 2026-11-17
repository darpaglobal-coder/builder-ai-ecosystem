# Remote Network & Decentralized Agent Operations

Status: architecture and implementation guardrails. No network discovery, remote access, device enrollment, powerline change or production command is authorized by this document.

## 1. Scope and trust boundaries

Operate only assets that the customer owns or is explicitly authorized to administer. Maintain an asset register containing owner, tenant, site, device class, serial/asset ID, network zone, firmware, support status, permitted protocols, safety impact and authorization evidence.

Never scan public address ranges, enumerate nearby networks, discover or enroll third-party devices, bypass authentication, propagate agents, install persistence, evade monitoring or interfere with communications. Unknown devices remain untrusted and untouched.

## 2. Reference topology

- Control plane: tenant, identity, policy, fleet inventory, approvals, task scheduler and audit.
- Regional control plane: jurisdiction-specific routing, data residency and failover.
- Site gateway: outbound authenticated connection, local queue, protocol adapters and signed updates.
- Device/edge layer: vendor-supported APIs and read-only telemetry by default.
- Agent runtime: isolated workloads with per-agent identity, resource quotas, signed code and explicit tool allowlists.
- Observability: metrics, traces, logs, security events and cost attribution.

Prefer outbound mutually authenticated TLS connections from site gateways. Do not expose management interfaces directly to the public internet.

## 3. Protocol compatibility matrix

| Technology | Supported role | Security/operational requirements |
|---|---|---|
| IPv4 | Addressing and routing | Private addressing, segmentation, firewall allowlists, no assumption that NAT is a security boundary |
| IPv6 | Addressing and routing | Explicit IPv6 firewall policy, RA/DHCPv6 protections, DNS consistency and dual-stack tests |
| DNS | Name resolution and service discovery | Managed zones, authenticated administration, DNSSEC where appropriate, protective filtering, split-horizon design where needed |
| SSH | Administrative access to owned hosts | Disable password login where feasible, keys/certificates, short-lived access, MFA-backed broker, host allowlist, session audit, no shared keys |
| UDP | Transport for approved services | Explicit ports/peers, rate limits, anti-spoofing, application-layer authentication and monitoring |
| TCP/HTTPS | APIs and reliable application transport | TLS, certificate rotation, authentication, request limits and schema validation |
| MQTT | Telemetry/event transport | TLS, per-client identity, topic ACLs, broker isolation, message expiry and replay protection |
| QUIC/VPN | Secure transport or private connectivity | Approved endpoints, key rotation, route restrictions and tested failover |

A protocol being technically compatible does not imply permission to connect to a network or device.

## 4. Powerline communications (PLC/BPL)

Treat powerline communications as a specialized, site-authorized link technology, not a way to access utility control systems. Before any pilot:
- Obtain written property-owner and, where applicable, utility/operator authorization.
- Use certified, supported equipment and vendor-approved configuration.
- Have a qualified electrical/communications professional assess electrical safety, isolation, grounding, surge protection, electromagnetic interference and coexistence.
- Review applicable FCC Part 15 and other local rules; maintain interference mitigation and shutdown procedures.
- Keep PLC data networks segregated from protection relays, breakers, SCADA and other safety-critical OT.
- Start with passive link-quality measurement; no switching, load control, meter tampering or grid command injection.
- Stop deployment on interference, unsafe conditions, unexplained traffic or authorization lapse.

Never provide remote commands that alter utility distribution, protective devices or electrical service without the utility/operator's approved engineering and operational process.

## 5. Free-space optical (FSO) and radio links

FSO requires line-of-sight planning, weather/fog fade analysis, eye-safety compliance, mounting/structural review, link budget, encryption and failover. Radio links require spectrum authorization or lawful unlicensed-band operation, interference assessment, power/antenna limits and jurisdictional certification. Do not jam, intercept, impersonate or transmit outside permitted bands or power limits.

## 6. Decentralized agent fleet

Every agent must have:
- Unique workload identity and named accountable owner.
- Signed immutable release, verified provenance and software bill of materials.
- Explicit tenant/site/resource scope and allowlisted tools.
- Read-only default; separate capability grants for each write action.
- CPU, memory, network, concurrency and spend quotas.
- Heartbeat, health checks, bounded retries, dead-letter queue and circuit breaker.
- Per-agent audit trail, version pinning, staged rollout and rollback.
- Immediate disable/revoke control and credential rotation.
- No self-registration, self-replication, privilege escalation or automatic discovery of external targets.

Agent-to-agent coordination uses authenticated event topics and typed schemas. Agents exchange task references and minimum necessary data, not shared credentials. High-impact actions require policy evaluation and human approval.

## 7. Remote task lifecycle

queued → policy check → assigned → approved (if required) → executing → verified → completed/failed → retained/expired.

Each task includes:
- task_id, requester, owner, target asset IDs, allowed operation, environment
- authorization proof, approval reference, deadline and maintenance window
- idempotency key, timeout, retry budget and rollback plan
- expected result, verification method, telemetry and cost center

Use bounded concurrency and backpressure. Offline sites queue only permitted tasks; commands that could become unsafe or stale expire rather than execute after reconnect. Never replay expired safety-sensitive commands.

## 8. Network change control

For DNS, routing, firewall, IPv4/IPv6, VPN and SSH changes:
1. Export current configuration and verify recovery access.
2. Open a change request with owner, scope, reason, risk and rollback.
3. Validate syntax and policy in a lab/staging environment.
4. Obtain required peer/security approval.
5. Apply to one canary site or host.
6. Verify health, access logs and expected routes/resolution.
7. Expand gradually with automatic stop conditions.
8. Close with evidence and post-change review.

No bulk edits or global changes based on guessed inventories.

## 9. Resilience and service levels

Design for regional isolation, local safe operation, encrypted store-and-forward, bounded queues, clock drift, duplicate delivery and idempotent consumers. Define availability objectives from measured service capacity. Do not promise 24/7 support or millisecond global execution without funded staffing, capacity tests and contractual SLAs.

## 10. Scale and performance

Treat very large fleet counts as capacity targets, not deployed devices or verified connections. Benchmark by tenant, site, messages/second, payload size, retention, concurrency, geographic latency and cost. Use synthetic test data first; enforce quotas and per-tenant fairness. Publish measured limits and saturation behavior.

## 11. Operational acceptance tests

- Identity and authorization denial tests for unknown devices and tenants.
- IPv4 and IPv6 segmentation and firewall tests.
- DNS change, rollback and DNSSEC validation where applicable.
- SSH short-lived credential, session logging and revocation tests.
- UDP rate-limit and spoofing-resilience tests.
- MQTT topic ACL, replay and certificate rotation tests.
- Gateway offline/online, queue expiry and duplicate delivery tests.
- Agent kill-switch, signed update, rollback and quota tests.
- PLC/FSO/radio safety and regulatory review before physical pilot.
- Cost, latency, packet loss, recovery and load tests with synthetic traffic.
