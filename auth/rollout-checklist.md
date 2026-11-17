# Google + Apple sign-in rollout checklist

Use this checklist per environment and per application. A checked item requires evidence (configuration export, test result, review record, or production health check), not an assumption.

## Platform foundation
- [ ] Owner confirms canonical auth domain and control of DNS.
- [ ] Production and staging HTTPS certificates are valid.
- [ ] Persistent database, backups, restore test, and encryption are configured.
- [ ] Server-side secret manager is configured; no secrets are committed.
- [ ] Auth broker has stable callback paths and strict return-URL allowlists.
- [ ] OIDC issuer, audiences, keys/JWKS rotation, session lifetime, logout, and revocation are documented.
- [ ] App registry contains every discovered and owner-authorized ORIN app surface.

## Google
- [ ] Owner-controlled Cloud project and OAuth consent configuration exist.
- [ ] Authorized domain and privacy/support URLs are verified.
- [ ] Web OAuth client exists.
- [ ] Exact HTTPS callback URI is registered.
- [ ] Client ID and secret are installed only in the server-side secret manager.
- [ ] Approved button uses current Google Identity Services / official assets.
- [ ] Sign-in uses only minimum scopes; optional APIs use incremental consent.
- [ ] Production consent/verification requirements are satisfied.
- [ ] Sign-in, cancellation, error, token expiry, revocation, and account-link tests pass.

## Apple
- [ ] Owner-controlled Apple Developer Program team is available.
- [ ] Primary App ID has Sign in with Apple capability enabled.
- [ ] A unique Services ID is registered and associated to the primary App ID.
- [ ] Canonical broker domain and exact absolute return URL are configured.
- [ ] Private key, Team ID, Key ID, and Services ID are in the secret manager.
- [ ] Server-side client-secret JWT generation and pre-expiry rotation are monitored.
- [ ] Approved Apple button/artwork and required title/color/shape rules are followed.
- [ ] Apple private-relay email and first-authorization-only email/name behavior are handled.
- [ ] Sign-in, cancellation, expiry, key rotation, revocation, and account-link tests pass.

## Tenant and account security
- [ ] Provider identity is keyed by issuer + subject, not email.
- [ ] Account linking requires fresh proof of control of both identities.
- [ ] Every protected API enforces tenant, brand, location, and role authorization on the server.
- [ ] Cross-tenant access tests fail closed.
- [ ] MFA/passkeys required for privileged roles.
- [ ] Abuse protection, rate limits, audit logs, alerting, and recovery are tested.
- [ ] User account export, unlink, deletion, and session revocation flows are tested.

## Copyright and trademark review
- [ ] ORIN application code and written content are original or appropriately licensed.
- [ ] Google and Apple sign-in assets follow their respective official brand guidelines.
- [ ] All franchise names/logos/photos/media have documented permitted use.
- [ ] No copied competitor code, proprietary UI, paid templates, or unauthorized datasets are included.
- [ ] Asset provenance, license, attribution, territory, and expiry are recorded.

## Release decision
- [ ] Independent security review completed.
- [ ] Privacy/legal review completed for target jurisdictions.
- [ ] Staging end-to-end tests pass for each app.
- [ ] Owner approves the production release.
- [ ] Production health checks and rollback plan are verified.

**Release state vocabulary:** planned → configured → tested → production-verified. Never collapse these states into a single "connected" status.
