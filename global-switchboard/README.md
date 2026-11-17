# ORIN Global Switchboard — Front-end prototype

This directory contains a static, responsive front-end prototype for a 195-workspace country switchboard.

## Inventory definition

The directory contains 193 UN Member States plus the Holy See and the State of Palestine (the two UN non-member observer states). The displayed count is therefore exactly 195 under this stated administrative definition. It is not a statement about diplomatic recognition, sovereignty, or permission to operate in any jurisdiction.

## Included

- Search by country name or ISO alpha-2 code
- Region filtering
- 195 country workspace entries and individual workspace inspection
- Standby-first status display
- Readiness gates for identity, data, workers, secrets, monitoring, recovery, legal approvals, and human escalation
- CSV export of the country inventory
- Responsive desktop and mobile layout

## Important deployment boundary

This is a static front-end only. It does not connect to a database, identity provider, queue, agent runtime, payment service, Cloudflare, country infrastructure, or external APIs. It does not activate services, execute background work, or provide unattended production operations. All 195 entries intentionally remain in standby.

Production autonomy requires separately implemented and secured backend services, country-by-country legal and operator authorization, least-privilege credentials, audit logging, monitoring, tested backup/recovery, incident response, and human approval for consequential actions. Do not represent the platform as 24/7 or self-sufficient until those services are deployed and verified.

## Preview

Open `index.html` in a browser or deploy this directory as a static preview after review.
