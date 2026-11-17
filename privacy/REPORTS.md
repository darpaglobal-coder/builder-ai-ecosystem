# ORIN privacy and security reporting standard

A report is required for each production application, website, domain, endpoint class, device fleet, AI agent, connector, and data processing workflow.

## Report statuses
- `not_assessed`: no evidence reviewed.
- `in_progress`: evidence gathering and review underway.
- `reviewed_with_findings`: review completed with remediation items.
- `approved_for_limited_purpose`: named purpose, data scope, owner, region and expiry approved.
- `blocked`: material risk or missing authority prevents processing.
- `expired`: approval/review window has elapsed.

No asset defaults to approved.

## Required report sections
1. Asset identity, owner, purpose and environment.
2. Source systems, data categories, data subjects and collection method.
3. Authorization and legal/contractual basis.
4. Data flow map, recipients, subprocessors and cross-border transfer details.
5. Authentication provider, OAuth scopes, agent service identity and permissions.
6. IPv4/IPv6 exposure, DNS, TLS, ports/services, evidence date and access restrictions.
7. Device enrollment basis, endpoint management, telemetry categories and opt-out/revocation.
8. AI agent model/provider, tools, prompt/data boundaries, logs, retention, evaluation and human oversight.
9. Security controls, encryption, secrets, access reviews, vulnerabilities and incident handling.
10. Retention, deletion, export, correction and user-rights processes.
11. Revenue and advertising data use, consent, disclosures, attribution and billing records.
12. Findings, severity, owner, due date, remediation evidence and next review date.

## Reporting protections

Never include passwords, OAuth tokens, private keys, raw secrets, full personal chat contents, wallet signing material, or unredacted private network topology in general reports. Use access-controlled evidence references and redacted summaries. Reports themselves are sensitive records and require tenant-scoped access.

## ChatGPT history

The platform cannot read every private ChatGPT conversation from the GitHub or Vercel project. Import only an export explicitly supplied by the account holder, scope the processing purpose, preserve source timestamps and attachments, and provide retention/deletion controls. Do not scrape the ChatGPT interface or use another person's conversation history.

## Device and agent inventory

Only inventory devices and agents from sources the owner controls and authorizes (for example, MDM, router, cloud account, source repository, or explicit registration). Do not perform broad network scans, install agents, or enroll hardware by inference.
