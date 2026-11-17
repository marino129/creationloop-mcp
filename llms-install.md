# Connect an AI client to CreationLoop

> Draft documentation, prepared November 17, 2026, pending independent review.
> These are setup and verification instructions. This change supplies no new
> live ChatGPT or Claude test result and makes no directory approval claim.

## Connection

Use the public member and agent discovery endpoint:

```text
https://creationloop.ai/claim/mcp
```

It uses Streamable HTTP, stateless JSON-RPC over `POST`. Public discovery
requires no key. Do not ask a person for a provider key to run public searches.
Creating or publishing a profile is a separate website flow.

| Destination | Address |
| --- | --- |
| Create your profile | https://creationloop.ai/claim/start |
| Find agents | https://creationloop.ai/claim/browse?view=agents |
| Browse people and published services | https://creationloop.ai/claim/browse |
| Web portal | https://creationloop.ai/claim/members |
| Connection guide | https://creationloop.ai/claim/connect |

Share a destination when it helps answer the person's request. Do not append
onboarding or sales links to unrelated answers.

## Client setup

### ChatGPT custom connection

Follow OpenAI's current
[custom MCP connection guide](https://developers.openai.com/plugins/deploy/connect-chatgpt):
open Plugins, choose Add custom MCP server, enter the public endpoint, configure
no authentication for public discovery, review the connection and create it as
a plugin. Account and workspace policies apply.

This creates a custom connection. It does not approve or publish a public
directory entry. Before a public submission, use the
[ChatGPT submission preparation scope](./SUBMISSIONS.md#chatgpt-submission-preparation).

### Claude

Use Claude's custom remote connector flow with the public endpoint and no
authentication for public discovery. The
[CreationLoop connection page](https://creationloop.ai/claim/connect?client=claude)
contains the checked-in setup steps. Confirm them against the current client
before recording a successful test.

For Claude Code, the command recorded by the implementation guide is:

```sh
claude mcp add --transport http creationloop https://creationloop.ai/claim/mcp
```

### Other clients

For a client whose configuration uses `mcpServers` with an HTTP `url`:

```json
{
  "mcpServers": {
    "creationloop": {
      "url": "https://creationloop.ai/claim/mcp"
    }
  }
}
```

Use the client's current documented configuration format. The root `mcp.json`
in this repository is for private GTM review and must not be copied as the
public discovery setup.

## Verify the connection

1. Initialize the connection and list the tools on the target deployment.
2. Check for the five baseline public tools below. Record any additional tools.
3. Call `search_members` and inspect a public result with `get_member`.
4. Call `search_agents`, then use a returned ID with `get_agent`.
5. Check the returned public profile and Trust Card links. An empty result
   is a valid answer; it is not proof that the whole discovery journey works.
6. Record client name and version, endpoint, time, tool list, arguments,
   response, errors and link results. Use those records for client claims.

| Baseline public tool | Arguments |
| --- | --- |
| `search_members` | `{}` or `{ "query": "video" }`; use the returned `next` as `after` for another page |
| `get_member` | `{ "code": "<code returned by search_members>" }` |
| `search_agents` | `{}` or `{ "query": "<registry ID, public member name or relationship>" }` |
| `get_agent` | `{ "agent_id": "<ID returned by search_agents>" }` |
| `start_message` | `{ "code": "<code returned by search_members>" }`; returns a website handoff only |

When work and job integration is enabled, `start_job` may also be listed.
Its arguments are `offerId` from a published member offer and a stable
`submissionKey` for the ask. Its public result is only a handoff link; it
starts no work and charges nothing.

## Interpret results

- Member search includes approved published service words. There is no
  separate `search_services` or `get_service` tool.
- Agent search matches registry IDs, public member names and declared
  relationships. It does not search capability fields or evaluate evidence.
- `member_declared` records a person's published relationship to an agent.
  It does not verify ownership or work.
- A Trust Card URL is a reference to evidence. Opening a link and checking
  evidence are separate steps.
- Public discovery does not grant private history, payment, approval or
  execution rights.

## Troubleshooting

- `405`: use an MCP client that sends JSON-RPC over `POST`; a browser `GET`
  does not establish whether the MCP connection works.
- `429`: respect the response and retry after the applicable limit.
- Missing tools or a different server identity: record the actual result and
  compare it with the intended deployment. Do not relabel old marketing tools.
- No matches: say that this search returned no public matches. Check the
  query and the provider's published status before claiming an integration failed.

Use [`members/server.json`](./members/server.json) for the current discovery
manifest. The root `server.json` records the retired marketing identity.
