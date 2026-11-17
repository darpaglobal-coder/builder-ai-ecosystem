# ORIN centralized identity foundation

**Status:** design and rollout contract only. No OAuth provider is configured or active.

## Verified scope and exact counts

| Item | Count | Meaning |
|---|---:|---|
| Requested external sign-in providers | 2 | Google and Apple |
| Current first-party web application surfaces verified in this repository | 1 | The static ORIN Global Switchboard front-end |
| Country workspace records in that switchboard | 195 | Tenant/workspace inventory entries, not 195 separate applications |
| Production identity brokers verified | 0 | None is deployed or connected |
| Working Google OAuth clients verified | 0 | Credentials and console configuration have not been supplied |
| Working Apple Services IDs verified | 0 | Apple Developer configuration and key have not been supplied |

The 195 workspace count is exactly the switchboard's stated definition: 193 UN Member States plus the Holy See and the State of Palestine. It is not a count of all franchises, brands, applications, or authorized markets. The repository currently proves one static web surface, not an inventory of every business app that might later connect.

There is no meaningful fixed maximum for all possible third-party applications or integrations. The system must count actual discovered, owner-authorized integrations in an application registry rather than invent a global total.

## Target architecture

Use one centrally operated ORIN identity broker on a domain controlled by the platform owner. It is the only Google/Apple OAuth client for first-party web sign-in. First-party applications authenticate against that broker through standards-based OpenID Connect (authorization code flow with PKCE); each application validates issuer, audience, signature, expiry, nonce, and approved redirect URI, then creates its own local session and tenant-scoped authorization context.

This avoids creating 195 unrelated login systems. Country workspaces are tenant records under the identity and authorization service. Franchise brands and franchisee operators remain separate tenants or explicitly governed sub-tenants.

**Web provider registrations (target):**
- One Google OAuth 2.0 Web application client for the central broker.
- One Apple Services ID for the central broker, associated with an eligible primary Apple App ID.
- One exact callback URI per provider on the canonical broker origin. Proposed paths below assume the Better Auth default callback path; confirm the selected framework and final hostname before registering them.
- Additional native iOS / Android client identifiers are separate platform registrations and are only created when actual native applications exist. They are not silently counted as active web apps.

**Proposed callback shape (replace the placeholder only after the canonical domain is owned and TLS verified):**
- Google: `https://<auth-domain>/api/auth/callback/google`
- Apple: `https://<auth-domain>/api/auth/callback/apple`

Do not register transient preview deployment URLs as production callback URLs. Google requires an exact authorized redirect URI match. Apple requires a registered Services ID, verified domain configuration, and an absolute return URL. Apple's documented Services ID website URL limit is 100 for organizations and 10 for individuals; a single shared broker origin keeps this design within that cap instead of registering one redirect for every country workspace.

## Authentication and authorization requirements

1. Use OAuth/OIDC authorization-code flow with PKCE, single-use state, nonce validation, HTTPS, strict redirect allowlists, secure same-site cookies, and server-side token validation. Never accept arbitrary post-login return URLs.
2. Treat provider identity as the immutable pair `(issuer, subject)`, not email. Do not auto-merge Google and Apple accounts solely because their email strings match. Require the user to authenticate to both accounts before linking them; support Apple's private relay addresses and missing email claims on subsequent Apple sign-ins.
3. Keep authentication separate from authorization. Enforce tenant, brand, location, employee, supplier, and administrator roles server-side on every request. Default new sign-ups to an unprivileged role and an unassigned tenant until an authorized invitation or approval assigns access.
4. Enable MFA / passkeys for privileged roles. Add recovery controls, session revocation, provider unlinking, login throttling, abuse detection, audit events, and alerting.
5. Request only `openid`, `email`, and `profile` where needed for sign-in. Do not request Drive, Gmail, Calendar, Contacts, payment, or other API scopes at login. Ask separately for the smallest additional permission at the moment a user activates a feature that needs it.
6. Encrypt provider refresh tokens and secrets at rest using a managed secrets / key service. Never place secrets in source control, browser bundles, logs, screenshots, issue comments, or this repository.
7. Define retention, deletion, export, incident response, breach notification, data residency, and privacy disclosures before enabling country or enterprise tenants.
8. Add tests for provider callback errors, expired/rotated tokens, nonce/state mismatch, replay, account-link conflicts, email changes, Apple private relay, disabled users, tenant boundary violations, and revoked sessions.

## Required credentials and owner actions

**Google**
- Create or select a Google Cloud project controlled by the platform owner.
- Configure the OAuth consent screen, verified domains, app name, support contact, privacy policy, authorized origins, and exact callback URI.
- Create a Web application OAuth client and store its client ID and secret in the server-side secret manager.
- Complete any required verification for requested scopes and production user volume.

**Apple**
- Have an eligible Apple Developer Program team and an existing primary App ID with Sign in with Apple enabled.
- Register a unique Services ID, associate it with the primary App ID, and register the canonical broker domain and exact return URL.
- Create an Apple Sign in with Apple private key and store the key securely. Record Team ID, Key ID, and Services ID.
- Generate and rotate the client-secret JWT server-side; never commit the private key or generated secret. Apple client-secret expiry must be tracked and renewed before expiry.

These accounts, identifiers, domain ownership, approvals, and secrets are not accessible from the present repository/Vercel connection. No credentials have been created or activated by this change.

## Integration into every ORIN surface

Every actual first-party web, mobile, admin, partner, workforce, marketplace, and franchise surface must be entered in a reviewed app registry with: immutable app ID, owner, production domain/bundle ID, platform, redirect/callback allowlist, OIDC audience, tenant model, data classification, privacy notice, security contact, release status, and test evidence.

Each app should use the central broker where technically appropriate. For third-party services, connect only where the service owner has granted access and its terms allow the integration. A provider option shown in an interface does not mean the external service is connected.

Before declaring an app integrated, verify sign-up, sign-in, sign-out, account linking/unlinking, recovery, revoked-session handling, tenant isolation, redirect allowlists, and audit events on that app's real production domain. Track `planned`, `configured`, `tested`, and `production-verified` as separate states.

## Copyright, trademarks, and brand safety

- Write original ORIN source code, copy, workflows, visual design, documentation, and database structure. Do not copy proprietary source code, competitor screens, paid templates, private datasets, or copyrighted marketing material.
- Use Google Identity Services or Google's approved current sign-in assets and follow Google's current button, logo, color, text, spacing, and prominence rules. Do not make an imitation Google button or imply Google endorses ORIN.
- Use Apple's official Sign in with Apple button component/artwork and follow Apple's title, logo, color, shape, and spacing requirements. Never redraw or improvise Apple's logo.
- Treat franchise and brand names, logos, product photography, menus, and marketing materials as third-party intellectual property. Display only factual names needed for identification unless the owner has granted permission or a documented license covers the asset and use. Do not imply affiliation, sponsorship, or endorsement.
- Maintain an asset register containing creator/source, license or permission, permitted uses, attribution obligations, territory, expiry, and takedown contact. Remove assets when rights are unclear or expire.
- Prefer original generic UI components and customer-provided / licensed brand assets. Do not scrape restricted sites or republish content without rights.

## Rollout gates

1. Select and verify the canonical auth domain and production hosting.
2. Provision a durable database and managed secrets; add a supported server runtime. The current switchboard is static HTML and cannot host a secure OAuth callback or persistent sessions by itself.
3. Implement the identity broker and tenant-aware OIDC relying-party contract.
4. Configure Google and Apple registrations using owner-controlled accounts.
5. Implement server-side authorization, audit, monitoring, backup, recovery, and privacy controls.
6. Test on a staging hostname with real provider credentials and test accounts.
7. Obtain independent security review and platform-owner approval, then deploy deliberately to production.
8. Enroll each additional application only after it passes the app registry and test gates.

**Do not describe sign-in as live, all apps as integrated, or the network as 24/7 until the production checks pass.**
