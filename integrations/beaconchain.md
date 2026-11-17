# Beaconcha.in connector — authorized analytics only

**Status:** connector specification only. No Beaconcha.in account, API key, validator ownership, or data permission is connected.

Official API entry point: https://www.beaconcha.in/api  
Official API pricing: https://www.beaconcha.in/pricing?product=api  
Official explorer: https://www.beaconcha.in/

## Intended capabilities

Subject to the API plan, terms, and owner authorization:
- Ethereum execution/consensus chain explorer data.
- Validator performance, status, duties, rewards and lifecycle analytics.
- Historical network and validator metrics.
- Authorized machine/validator monitoring.
- Alerts and webhooks where supported by the selected plan.
- Internal dashboards, benchmarking and customer reports where the license permits.

## Commercial-use gate

The current published pricing table distinguishes API plans. The listed Free Trial, Hobbyist, Business and Scale tiers do not include commercial-use rights; Enterprise lists commercial use and a custom SLA/rate limits. Attribution terms vary by plan. Do not resell, redistribute, or embed Beaconcha.in data in a paid ORIN product until the selected plan and written terms expressly permit the intended use. Verify current pricing and terms at procurement time; do not purchase or contact the vendor automatically.

## Security and privacy

- API key stored in a managed secret manager; never in Git, browser code, logs, reports or prompts.
- Use only authorized validator identifiers and accounts.
- Keep public chain data distinct from user account, device, wallet ownership, and personally identifying data.
- Do not infer ownership of a validator or wallet from public on-chain data.
- Do not initiate staking, signing, transfers, withdrawals, validator changes or financial transactions.
- Track API request volume, rate limits, plan cost, attribution and retention.
- Cache within the permitted terms; back off on rate limiting; log source timestamps and data freshness.
- Mark missing, delayed, estimated and unverified values explicitly.

## Monetization options

Only after written commercial-use rights and customer contracts:
- Paid validator operations dashboards.
- Validator uptime and performance reporting.
- Enterprise network analytics.
- Licensed API-backed benchmarking.
- Managed monitoring and alerting.

Never guarantee staking yield, validator rewards, token prices, investment returns, or a specific revenue outcome.
