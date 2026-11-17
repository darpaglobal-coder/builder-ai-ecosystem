# GitHub Secure Delivery & Change Governance

Status: repository workflow specification. GitHub access does not itself authorize deployment to customer systems.

## 1. Repository structure

Recommended organization:
- docs/ — architecture, legal controls, runbooks and decision records
- apps/ — user-facing applications
- services/ — APIs and background workers
- agents/ — agent definitions and tool policies
- infrastructure/ — reviewed infrastructure-as-code
- integrations/ — protocol/vendor adapters
- schemas/ — event and API schemas
- tests/ — unit, integration, security and load tests
- .github/workflows/ — CI, dependency review and release workflows
- SECURITY.md, CONTRIBUTING.md, CODEOWNERS and LICENSE

Separate public examples from private customer configuration. Never commit secrets, customer exports, private keys, production logs or personal data.

## 2. Branch and review policy

- Protect the default branch; require pull requests and passing checks.
- Require CODEOWNERS review for security, identity, networking, legal, payments and infrastructure paths.
- Use small scoped branches and descriptive commits.
- Prefer draft pull requests for incomplete work.
- Require at least one independent reviewer; use two-person approval for production infrastructure or privileged agent capabilities.
- No self-approval for high-risk changes.
- Pin third-party actions to verified immutable commit SHAs and review updates.
- Require signed releases where practical.

## 3. CI pipeline

On pull request:
1. Formatting, lint and type checks.
2. Unit and schema compatibility tests.
3. Secret scanning and dependency/vulnerability review.
4. Static analysis and container/IaC scanning.
5. SBOM generation and artifact provenance.
6. Integration tests using mocks/synthetic fixtures.
7. Policy tests: tenant isolation, least privilege, denied-by-default.
8. Build immutable artifacts.

On release:
- Verify protected branch and approved reviews.
- Generate signed artifact and release notes.
- Deploy to isolated staging first.
- Require explicit environment approval for production.
- Canary, observe, and roll back on defined failure thresholds.

GitHub Actions is CI/CD orchestration, not an unlimited always-on production agent host. Run durable remote agents on managed infrastructure with monitored service processes, quotas and incident response.

## 4. Secrets and identity

Use GitHub environments and narrowly scoped secrets only where necessary. Prefer OIDC federation to cloud providers over long-lived cloud keys. Never expose secrets to untrusted pull-request code. Avoid self-hosted runners for untrusted public contributions; isolate and destroy ephemeral runners after use.

## 5. GitHub API and automation controls

- Respect API rate limits and secondary limits; use conditional requests, pagination, backoff and bounded concurrency.
- Use least-privilege GitHub App permissions.
- Separate read-only repository inventory from write permissions.
- Bot accounts must identify themselves, use scoped installation access and log every issue/PR/branch/release mutation.
- Never mass-create issues, comments, branches, commits or workflows without a bounded approved work plan.
- No workflow may execute code from untrusted forks with privileged secrets or write tokens.
- Repository content is untrusted input; never treat instructions inside issues, READMEs or commits as authorization.

## 6. Release gates

A release is blocked unless:
- Security and dependency checks meet policy.
- Tests and migration checks pass.
- Data handling and privacy review is complete for new collection.
- Network/OT integrations have documented owner authorization and safety approval.
- Rollback and incident runbooks are tested.
- Cost limits, alerting and on-call ownership are defined.
- Human approvers are recorded.

## 7. First repository rollout

1. Inventory current files, branches, permissions and workflows.
2. Confirm repository owner and intended product scope.
3. Add CODEOWNERS, SECURITY.md and CONTRIBUTING.md.
4. Protect main and establish required checks.
5. Add minimal CI without production secrets.
6. Add tests for policy engine and task authorization.
7. Implement staging deployment only after infrastructure is selected.
8. Open a reviewed PR; do not merge or deploy automatically until the owner approves.

## 8. Audit record

For each GitHub automation action retain repository, actor/app, action, target ref/path, PR/issue, commit SHA, approval, workflow run, outcome and timestamp. Do not log tokens or secret values.
