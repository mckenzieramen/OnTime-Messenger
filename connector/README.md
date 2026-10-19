# OnTime Windows Connector (design stage)

This folder documents a future Windows agent; it does not currently communicate with personal Messenger.

The planned agent will:
- run locally under the user's Windows account;
- establish an outbound TLS connection to a Cloudflare-protected API;
- authenticate using a dedicated service credential stored outside the repository;
- report only health/online status until a supported provider adapter exists;
- require explicit consent before accessing any local application data.

Do not enter Facebook credentials, session cookies, or private tokens into the OnTime website. Do not expose an unauthenticated remote-control API on your PC.

See ../ARCHITECTURE.md.
