# CreationLoop: the Better Agent Bureau

**Proving the value of your agents' work.**

> Draft documentation, prepared November 17, 2026, pending independent review.
> This update describes the source and the intended connection path. It does
> not establish a deployment, a tested client connection or directory approval.

If you offer AI agents to customers, give them a place to check the work, the
results and the evidence. CreationLoop connects public agent references, the
people who list them and their Trust Cards.

The public discovery API also finds members and the services they have
published. It reads the public information they chose to show. An agent's
Trust Card carries separate evidence about its work.

## Start here

| What you want to do | Link |
| --- | --- |
| Create your profile | [Create your profile](https://creationloop.ai/claim/start) |
| Find agents and their people | [Find agents](https://creationloop.ai/claim/browse?view=agents) |
| Find people and their published services | [Browse CreationLoop](https://creationloop.ai/claim/browse) |
| Open the web portal | [Sign in](https://creationloop.ai/claim/members) |
| Connect your AI | [Connection guide](https://creationloop.ai/claim/connect) |

Creating a profile does not publish it automatically. Public discovery uses
approved, visible, published profiles and offers. The links above point to the
web product. This draft includes no mobile app store or download claim.

## Connect to public discovery

- **Endpoint:** `https://creationloop.ai/claim/mcp`
- **Transport:** Streamable HTTP, stateless JSON-RPC over `POST`
- **Public discovery:** no key required
- **Source server identity:** `creationloop-members`, version `1.2.0`
- **Registry manifest:** [`members/server.json`](./members/server.json), name `ai.creationloop/members`

Use the [agent install guide](./llms-install.md) for setup and verification.
The manifest is copied from the current Claim source. Its presence here does
not publish it to a registry or make the server available to every AI client.

## What the current public tools do

| Tool | Input | Result |
| --- | --- | --- |
| `search_members` | Optional `query`, `after` | Find public member cards. Search includes published service titles, scope, terms and prices. |
| `get_member` | `code` | Read one public member card, its published offers and the profile link. |
| `search_agents` | Optional `query`, `after` | Find published agent references by registry ID, public member name or declared relationship. |
| `get_agent` | `agent_id` | Read one published agent reference, its linked public people and its Trust Card link when available. |
| `start_message` | `code` | Get a website link for a person to review the member's terms and write a message. The tool sends nothing and spends nothing. |

`start_job({offerId, submissionKey})` is an additional public tool when the
deployment enables the work and job integration. It returns a website link
where the person can review the offer and start a job. The public tool starts
nothing and charges nothing. Confirm the actual tool list on the target
deployment; five baseline tools does not mean exactly five in every deployment.

These tool descriptions document the existing general endpoint. A public
ChatGPT submission needs its own reviewed discovery and evidence scope; see
[submission preparation](./SUBMISSIONS.md#chatgpt-submission-preparation).

## Read the evidence accurately

A listed agent returns an `agent_id`, the public people linked to it and an
`association_status` of `member_declared`. Each person supplies their
relationship on an approved profile. That relationship alone does not prove
ownership or completed work.

The canonical Trust Card address is
`https://creationloop.ai/verified/registry/<agent_id>`. Discovery returns a link
when available; it does not fetch the evidence, check a receipt or assign a
verification score. Report a missing card or an empty result plainly.

Published service offers currently appear on member cards. They include the
offer ID, version, title, scope, delivery period, terms and price fields. There
is no separate `search_services` or `get_service` tool, and this public offer
shape does not bind a service to an agent. Agent search does not currently
search an agent's capabilities or Trust Card evidence.

Useful requests include:

- "Find providers with published video production services on CreationLoop."
- "Show the agents this provider lists and the people linked to them."
- "Open this agent's Trust Card so I can inspect the evidence."

## Connection and publication status

The implementation was reviewed at `creationcode@7deffe4ea49864144bc10045f7eedf1425aa21e9`.
This is a source reference, not a receipt for what is running.

A read-only HTTP probe on November 17 at 21:00:20 UTC returned the five baseline
public tools above. `start_job` was not returned on that anonymous surface.
Later public reads found an agent reference and confirmed that the profile,
connection and agent browse pages returned HTTP 200. These are endpoint checks,
not a ChatGPT or Claude client acceptance test.

The checked-in guide records narrower historical calls in Claude Code
(October 19) and a Claude custom connector (October 28). Those records do not
test the current agent and service discovery journey. This documentation
update did not repeat them or run a current ChatGPT or Claude connection test.

Custom connection, directory submission, approval and successful use are
separate milestones. Current directory observations and the work still needed
are recorded in [SUBMISSIONS.md](./SUBMISSIONS.md).

## Historical files in this repository

The root [`server.json`](./server.json) belongs to the retired marketing
server, `ai.creationloop/creationloop`, at `https://creationloop.ai/api/mcp`.
It remains unchanged to preserve that identity. Use `members/server.json`
when preparing the member discovery registration.

The root [`mcp.json`](./mcp.json) and
[`.cursor-plugin/plugin.json`](./.cursor-plugin/plugin.json) configure a
separate private GTM review tool. They are not the Bureau discovery
configuration. Their protected token setup is for authorized operators.

The separate CreationCode build connector drafts in pull requests
[1](https://github.com/marino129/creationloop-mcp/pull/1) and
[2](https://github.com/marino129/creationloop-mcp/pull/2) are outside this
discovery setup.

## License

This repository's documentation and configuration use the
[MIT License](./LICENSE).
