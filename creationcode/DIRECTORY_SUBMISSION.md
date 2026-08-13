# Directory submission material — blocked draft

## Listing copy

**Name:** CreationCode

**Short description:** Turn an exact human-approved Request into one bounded build, verified pull request and Receipt.

**Long description:** CreationCode lets Claude and Claude Code guide a software job through one trusted lifecycle: non-authoritative conversation, exact Final Request, Plan and cost review, direct human approval, one bounded Claude Code run, pull request, exact-SHA merge approval, independent verification and Receipt. OAuth and repository binding stay server-side. GitHub credentials never reach the coding executor or client.

**Category:** Developer tools / software delivery / governance

**Transport:** Remote modern Streamable HTTP, MCP 2026-07-28

**Authentication:** OAuth 2.0 resource server (provider pending founder decision)

**Repository:** <https://github.com/marino129/creationloop-mcp>

**Endpoint:** `https://creation-code.replit.app/mcp` — placeholder; do not submit until the route is deliberately activated and proven.

## Review notes

- Three consequential tools always require direct human review in CreationCode.
- One ratified Plan can reserve at most one run across retries/hosts/concurrency.
- Merge approval binds repository, PR, base branch, exact candidate SHA and current checks.
- Receipt is derived only after an independent GitHub reread.
- Five interactive views retain the same Job, Plan, cost, run, PR/SHA and Receipt identifiers.

## Submission sequence after launch approval

1. Replace fixture screenshots with real Claude client captures and confirm all privacy copy.
2. Rename/copy `server.draft.json` to the publisher-approved manifest location and validate against the current official schema.
3. Verify endpoint discovery, OAuth and all listed tools from a normal external network.
4. Authenticate `mcp-publisher` for the `io.github.marino129` namespace and publish only after explicit founder approval.
5. Confirm the registry entry, then submit identical reviewed copy to approved directories.
6. Record submission URLs/status and monitor support/security contacts.

Official registry guide: <https://github.com/modelcontextprotocol/registry/tree/main/docs/guides/publishing>.
