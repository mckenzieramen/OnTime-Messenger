# OnTime remote connector architecture

## Current status
The deployed site is a local-only UI demo. It is NOT connected to a personal chat provider.

## Proposed components
1. Cloudflare Pages hosts the white/yellow OnTime interface.
2. Cloudflare Access restricts the entire dashboard to approved identities.
3. Cloudflare Pages Functions (or Workers) handle authenticated API calls.
4. A Windows agent connects outbound to a protected API using a dedicated service credential.
5. D1 stores only minimal connector state, with retention limits; R2 can store attachments if an authorized provider integration becomes available.

## Security requirements
- Do not publish personal chats, account passwords, cookies, browser sessions, or access secrets in GitHub.
- No direct public endpoint to the Windows computer; use outbound authenticated connections.
- Use separate service credentials for the Windows agent and human login for the dashboard.
- Verify authorization on every API operation; implement rate limits, audit logs, and revocation.
- Avoid exposing private message contents in logs or browser localStorage.
- Treat any provider adapter as optional; never claim successful message delivery without provider confirmation.

## Personal account integration feasibility
Meta's Messenger Platform API supports Facebook Pages, not full personal Messenger inbox control. No supported adapter for personal account chats, photos, or calls has been implemented. The Windows agent cannot change this API restriction.

## Delivery stages
1. Secure dashboard access using Cloudflare Access.
2. Authenticated agent heartbeat and online/offline indicator.
3. Local mock adapter and end-to-end tests across devices.
4. Only if a lawful, authorized and technically supported messaging adapter is available, enable real message sync.
5. Evaluate calls separately; do not imply calls work through the message adapter.

## Deployment
Existing root index.html is a static Pages asset. Build command blank, output directory ".". Dynamic functions require a functions/ directory and Cloudflare configuration. Access and service tokens must be configured in the Cloudflare dashboard; no secrets belong in this repository.
