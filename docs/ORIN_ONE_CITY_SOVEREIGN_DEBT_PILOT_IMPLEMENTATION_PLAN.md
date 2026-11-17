# ORIN One-City Sovereign Debt-Reduction Pilot
## Lawful implementation plan, AI-agent roles, filters, and prerequisites

**Pilot scope requested:** one city.
**Named city / jurisdiction:** NOT YET SELECTED. “230 million cities” is not a valid single jurisdiction and is not treated as a real-world city count. It is retained only as a synthetic scalability target for load testing.
**Operating mode until approvals:** read-only discovery, analysis, drafting, and sandbox simulation.
**Funding model:** no donations. All production work must be covered by an approved public procurement contract, subscription, or other lawful earned-revenue agreement. No public borrowing or unfunded reward promises are treated as ORIN revenue.
**Current deployment truth:** ORIN has a Vercel UI preview and GitHub design documents. It has no live municipal, treasury, billing, legal, banking, tax, procurement, document-management, or utility integrations. No government has authorized the pilot.

## 1. Pilot objective

Help one consenting municipal government identify and independently verify opportunities to improve fiscal transparency, reduce avoidable operating costs, strengthen lawful revenue administration, improve asset and project performance, and assess debt-service risks. The pilot does not promise debt elimination or a predetermined percentage reduction. It does not borrow, refinance, restructure, tax, procure, pay, enforce, or change public services on behalf of the city.

## 2. Required scope decision

Before real-world onboarding, the city must be named and its legal jurisdiction confirmed:
- city/municipality legal name and country;
- state/province/region and national legal system;
- sponsoring department and accountable public official;
- municipal legal entity and any included utilities/public corporations;
- written authority for data access and pilot activity.

Do not infer that the user's approximate location is the selected pilot city. Do not use “230 million cities” as a jurisdiction. If no city has consented, use a synthetic city dataset only.

## 3. Pilot phases and deliverables

### Phase 0 — sponsor and authority
Deliverables: sponsor letter; defined public purpose; procurement route; legal authority map; data controller/processor roles; conflict disclosures; pilot charter; named accountable officials; scope and exclusions.

Gate: written authorization from the municipality and procurement/legal sign-off.

### Phase 1 — read-only data inventory
Potential sources, only if lawfully provided:
- adopted budgets and in-year budget execution;
- audited financial statements and annual reports;
- debt register, guarantees, leases, arrears and contingent liabilities;
- procurement plans, tenders, contracts, amendments and vendor master data;
- public asset and capital-project registers;
- utility consumption and service-performance aggregates;
- payroll/workforce aggregates only where necessary and lawfully accessible;
- revenue collection aggregates, not unrestricted personal taxpayer data.

Deliverables: source catalogue, data dictionary, provenance register, coverage report, quality exceptions, privacy and retention schedule.

Gate: data-sharing agreements, lawful basis, least-privilege access, security review, data residency and retention approval.

### Phase 2 — fiscal baseline and risk map
Classify direct debt, guaranteed debt, public-corporation liabilities, leases, arrears and contingent liabilities without double counting. Record currency, rate, maturity, creditor class, covenants, payment schedule and legal authority. Reconcile budget, audited accounts and debt records. Distinguish stock from cash flow and gross from net measures.

Deliverables: reconciled baseline, debt maturity profile, interest/revenue indicators, gross financing needs, contingent-liability map, uncertainty register and independently reviewable calculations.

Gate: municipal finance officer and independent auditor accept the baseline or formally document limitations.

### Phase 3 — opportunity screening
Screen for:
- procurement price/volume anomalies and avoidable contract duplication;
- energy and building efficiency with metered baselines;
- fleet, routing, inventory and maintenance efficiency;
- project delay, change-order and lifecycle-cost risks;
- lawful revenue-administration gaps and billing-record inconsistencies;
- underused public assets where title, public purpose and legal constraints are verified;
- local supplier and SME productivity opportunities.

Each opportunity must state baseline, method, gross benefit, implementation cost, net benefit, time horizon, risk, service impact, distributional impact and verifier. No assumed saving is booked as realized cash.

Gate: city finance, legal, procurement, service owner and independent assurance approve a bounded pilot work order.

### Phase 4 — controlled pilot execution
Run approved, reversible interventions only. Use procurement rules and signed contracts. Keep source records immutable. Separate requester, implementer, verifier and payment approver. ORIN does not initiate payments or make award decisions. Pay vendors only under the city's existing authorized payment controls after acceptance and appropriation checks.

Deliverables: work orders, evidence receipts, acceptance records, exception log, cost ledger and outcome report.

### Phase 5 — evaluation and scale decision
Compare results with the agreed baseline and control group or matched period where feasible. Publish net realized benefit, service quality, complaints, workforce impacts, implementation cost, and audit findings. Expand only after public authority approval and independent evaluation.

## 4. AI-agent roster

All agents are tenant-scoped and least-privileged. Default access is read-only. Agents cannot approve contracts, alter tax liabilities, make legal determinations, execute payments, issue debt, change public services, or contact creditors as the municipality.

| Agent | Allowed tasks | Prohibited actions |
|---|---|---|
| Billing and receivables analyst | Reconcile authorized aggregate billing, invoices, receivables, duplicate records, billing-system exceptions; draft exception cases | Change rates, create charges, penalize accounts, access unnecessary personal data, collect money |
| Legal research and compliance assistant | Retrieve jurisdiction-specific statutes supplied/approved by counsel; cite sources; prepare issue lists and draft templates | Give binding legal opinions, serve notices, represent the city, determine liability or enforce |
| Document intelligence agent | OCR, classify, extract clauses and metadata from authorized contracts, budgets, audits and policies; preserve page/source references | Alter originals, fabricate records, publish confidential documents |
| Debt and treasury analyst | Reconcile debt schedules, maturity/currency/rate exposures and contingent liabilities; produce scenarios | Borrow, trade, refinance, restructure, pledge assets or contact creditors |
| Procurement integrity analyst | Detect duplicate invoices, unusual amendments, concentration and price outliers; explain false-positive risk | Select vendors, disqualify bidders, award contracts or allege wrongdoing as fact |
| Asset and project analyst | Match asset registers, maintenance, utilization and project milestones | Sell, transfer, operate or physically control public assets |
| Energy and operations analyst | Analyze authorized meter and service aggregates; propose efficiency tests | Control grid/SCADA/PLC or safety-critical equipment |
| Revenue policy analyst | Analyze aggregate revenue trends and administrative leakage; model lawful options | Set taxes, change tax policy, assess individual tax, or enforce |
| Privacy and data-governance agent | Detect sensitive fields, minimize datasets, track consent, retention and access | Override legal holds, erase audit evidence or grant access |
| Independent verification assistant | Check evidence completeness, calculations, duplicate claims and source traceability | Modify source data, implement the work, approve its own evidence or release funds |
| Public reporting and translation agent | Draft accessible reports and translations with uncertainty labels | Publish without authorized human review; certify legal translations |
| Billing/contract operations agent for ORIN itself | Track ORIN subscription invoices and contracted service usage | Mix ORIN commercial revenue with municipal treasury funds or fabricate billable usage |

Human review is mandatory for legal, tax, employment, procurement, credit, safety, public communication, and payment decisions. Agent output must include source citations, model/version, timestamp, confidence, and reviewer status.

## 5. Data and evidence controls

Every record must include tenant, source owner, legal basis, source URL or document ID, collection time, reporting period, currency/unit, license, sensitivity class, retention period, checksum where appropriate, and transformation history. Keep original source documents immutable. Corrections are append-only and attributable.

Evidence receipt fields: task ID; authorized scope; responsible human; agent/version; source IDs; action log; before/after evidence; timestamps; calculation; verifier; approval; exceptions; and final disposition.

Quarantine incomplete, stale, conflicting, unlicensed, unauthorized, or unverifiable data. Do not scrape protected portals or bypass login, rate limits, paywalls, or access controls.

## 6. Legal and governance prerequisites

The municipality and its counsel must assess, at minimum:
- constitutional and statutory municipal powers;
- public finance, debt-management and fiscal-responsibility rules;
- budget appropriation and borrowing authorization;
- public procurement and competitive tender requirements;
- records, archives, public-records and freedom-of-information rules;
- privacy, data protection, cybersecurity and cross-border transfer rules;
- tax/billing due process and appeal rights;
- labor, collective bargaining and worker classification;
- accessibility, language access and public participation;
- anti-bribery, conflicts of interest, sanctions and AML obligations where applicable;
- intellectual property, software licensing and open-source obligations;
- insurance, indemnity, liability, audit and dispute resolution;
- sector-specific requirements for utilities, transport, health, safety and critical infrastructure.

The exact list and required approvals vary by jurisdiction. Local counsel must validate before any live data or operational use. International good-practice references are not a substitute for local law.

## 7. Commercial model — no donations

Permitted candidate revenue, subject to local procurement and ethics rules:
- fixed-fee implementation and integration contract;
- fixed or tiered subscription for analytics and workflow;
- competitively procured managed-service contract;
- disclosed usage fees under a signed agreement;
- performance fees only if expressly lawful, competitively procured, independently verified, based on net realized savings, capped, and not tied to tax penalties, layoffs, service cuts, debt stock, or asset seizure.

No payment for projected savings, unaccepted deliverables, fabricated usage, phantom workers, or unfunded tasks. Do not treat public debt proceeds as earned ORIN revenue. Keep separate books, bank accounts and audit trails.

## 8. Security and operational requirements

- Dedicated municipal tenant and segregated data stores.
- SSO/MFA, role-based access, least privilege and short-lived credentials.
- Encryption in transit and at rest; managed key rotation.
- Private network paths and allowlisted integrations.
- Immutable audit events and monitored privileged access.
- No autonomous network discovery outside explicit written scope.
- No agent installation on third-party devices without owner authorization.
- No access to payment execution, tax enforcement, HR decisions or critical infrastructure control.
- Backups, recovery objectives, incident response, vulnerability management and independent penetration test.
- Human-operated support and escalation; do not advertise 24/7 until staffed and tested.
- Export, deletion and termination procedures consistent with records-retention law.

## 9. Pilot scorecard

Measure separately:
1. data coverage and reconciliation rate;
2. number/value of validated opportunities (not savings);
3. approved work orders and implementation cost;
4. independently verified gross savings or incremental lawful receipts;
5. net realized cash benefit after all costs;
6. debt-service and refinancing-risk changes, if any;
7. service availability/quality and complaint rates;
8. labor, equity, privacy and environmental effects;
9. audit exceptions, false positives and remediation time.

Do not count an accounting reclassification, asset valuation, avoided hypothetical cost, unpaid invoice, tax penalty, or forecast as cash saved. Do not count the same benefit twice.

## 10. Scale architecture and the 230-million target

Use 230 million only as a synthetic load-test target for logical records or entity references. It does not represent 230 million verified cities, governments, customers or connections. Use synthetic data marked TEST; never generate fake public debt, residents, officials, vendors, invoices or approvals. Real deployment remains one city at a time, with a separate mandate and tenant for each jurisdiction.

## 11. Immediate prerequisites checklist

- [ ] Name one real city and full legal jurisdiction.
- [ ] Identify a municipal sponsor and accountable finance official.
- [ ] Obtain written authorization and define public purpose.
- [ ] Confirm procurement route, budget and no-donation commercial contract.
- [ ] Obtain local legal, privacy, records and procurement review.
- [ ] Sign data-sharing / processor agreements.
- [ ] Approve read-only data sources and data dictionary.
- [ ] Complete threat model, security review and incident plan.
- [ ] Define baseline, metrics, verifier and audit access.
- [ ] Approve human decision rights and prohibited actions.
- [ ] Start with read-only pilot; no payment execution or debt transactions.
- [ ] Independently evaluate before any expansion.

## 12. Current state and next required decision

This plan is a proposed implementation blueprint committed to the ORIN GitHub feature branch. It has not been adopted by a municipality. No city has been selected, no municipal data has been accessed, no legal approvals have been granted, and no live AI agents or billing/legal/document integrations have been connected.

**Required next input:** the exact city and country (and state/province if applicable). Until then, only synthetic-data design and read-only architecture work can proceed.
