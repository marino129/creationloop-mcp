# Connect Claude and Claude Code (post-activation only)

Do not follow these steps until the launch checklist is complete and the founder has explicitly approved the public endpoint.

## Claude web and Desktop remote connector

Anthropic's current remote-connector flow is account-brokered and reaches the server from Anthropic's cloud. The endpoint must therefore be publicly reachable from the documented Anthropic network ranges.

For individual Free, Pro, or Max accounts:

1. Open **Customize → Connectors**.
2. Select **+ → Add custom connector**.
3. Enter the reviewed public CreationCode MCP URL.
4. Add approved OAuth client settings only if the deployment contract requires them.
5. Connect, review the requested scopes, and authenticate.
6. Enable CreationCode for an isolated test conversation.

For Team or Enterprise, an Owner or Primary Owner first adds the Web custom connector under **Organization settings → Connectors**; each member then connects individually.

Reference: [Anthropic remote custom connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

## Claude Code

After the endpoint is live in authorized staging:

```sh
claude mcp add --transport http creationcode https://APPROVED-HOST.example/mcp
```

Then start Claude Code and run:

```text
/mcp
```

Complete the browser OAuth flow, inspect the connected identity and scopes, and list the ten tools. Do not add a static bearer token or GitHub credential with `--header`.

Reference: [Claude Code MCP documentation](https://docs.anthropic.com/en/docs/claude-code/mcp).

## Verification prompt

Start with read/non-authoritative behavior only:

```text
Start a CreationCode conversation for my already-bound test repository, retain this message, and prepare—but do not submit—the exact Final Request.
```

Confirm that the same repository and job identifiers appear in the terminal fallback and the Final Request view. Do not exercise submission/build/merge until the staging test account and approvals in `TEST_ACCOUNT.md` are ready.
