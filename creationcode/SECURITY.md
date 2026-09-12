# Security and human-approval model

CreationCode applies four independent controls:

1. OAuth verifies signature, issuer, resource/audience, time, client, tenant and closed scopes.
2. The server resolves the GitHub installation, repository and base branch; client arguments cannot select them.
3. Request submission, paid build approval and merge approval require a trusted-origin, direct-human, single-use grant bound to exact hashes, cost and current state.
4. Durable idempotency and the domain reservation prevent duplicate mutations; failed mutations are retained and never silently retried.

Claude narration, MCP annotations, a rendered button, or a host saying “approved” is not authority. Views link to CreationCode for review; rendering alone cannot issue a grant.

The bounded executor receives no GitHub credential. CreationCode opens the PR. One exact-SHA merge attempt may occur only after direct approval, and an independent GitHub reread must prove it before a Receipt is derived.

If any output exposes a token/credential, accepts a stale/cross-binding grant, starts a second run, attributes the wrong merge, or produces a Receipt without independent evidence: disable the connector, preserve correlation IDs without copying secrets, revoke the connection, and follow `SUPPORT.md`.

Security reports should use a private GitHub security advisory, not a public issue: <https://github.com/marino129/creationloop-mcp/security/advisories/new>.
