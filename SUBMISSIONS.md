# CreationLoop discovery distribution

> Draft preparation record, November 17, 2026, pending independent review.
> This change updates documentation only. It submits no directory listing,
> publishes no registry record and changes no running service.

## Product and connection

**CreationLoop: the Better Agent Bureau.**

The current member discovery source finds public providers, their published
services, agent references and Trust Card links. The next distribution pass
must use those capabilities accurately and give providers a clear path to
create a profile.

| Field | Current value |
| --- | --- |
| Public endpoint | `https://creationloop.ai/claim/mcp` |
| Transport | Streamable HTTP, stateless JSON-RPC over `POST` |
| Public authentication | No key |
| Source server identity | `creationloop-members`, version `1.2.0` |
| Registry name to prepare | `ai.creationloop/members` |
| Current manifest | [`members/server.json`](./members/server.json) |
| Create your profile | https://creationloop.ai/claim/start |
| Find agents | https://creationloop.ai/claim/browse?view=agents |
| Browse people and published services | https://creationloop.ai/claim/browse |
| Web portal | https://creationloop.ai/claim/members |
| Connect your AI | https://creationloop.ai/claim/connect |

The manifest is copied from Claim source at
`7deffe4ea49864144bc10045f7eedf1425aa21e9`. Source presence is separate from
deployment and registration. Verify the profile flow and links on the target
deployment before advertising a completed instant onboarding journey.

## Read-only live checks

On November 17, 2026, at 21:00:20 UTC, a public HTTP `tools/list` request to
`/claim/mcp` returned HTTP 200 and the five baseline tools: `search_members`,
`get_member`, `start_message`, `search_agents` and `get_agent`. Optional
`start_job` was absent from that anonymous response. The descriptions still
include member payment wording, so the ChatGPT scope review below remains open.

At 21:02:07 UTC, public reads also confirmed:

- `search_agents({})` returned one public agent reference with a Trust Card
  link, no next page and `truncated: false`.
- `search_members({query: "agent"})` returned two profiles with empty `offers`
  arrays. This bounded query does not establish the service count of the catalog.
- `/claim/start`, `/claim/connect` and `/claim/browse?view=agents` returned
  HTTP 200. The live connection page included `/claim/start` and no
  `/claim/waitlist` link. No App Store or Play Store links appeared on those pages.

These checks do not establish a connected ChatGPT or Claude journey, client
approval, capability matching or a completed first Loop. No private profile
contents or prices are reproduced here.

## Observed distribution status

These are November 17 observations and historical records, not a claim that
the new Bureau offer is installed everywhere. A search that returns no record
does not prove that no record can exist.

| Destination | Evidence and observed state | Next action |
| --- | --- | --- |
| Official MCP Registry, retired identity | [Exact-name search](https://registry.modelcontextprotocol.io/v0.1/servers?search=ai.creationloop/creationloop) returned `ai.creationloop/creationloop`, version `0.1.0`, active and latest, published July 9, 2026, using `/api/mcp`. | Prepare the distinct members registration; do not publish the root legacy manifest as the new offer. |
| Official MCP Registry, current identity | [Members search](https://registry.modelcontextprotocol.io/v0.1/servers?search=ai.creationloop/members) returned zero records in this sweep. Current publication is not established. | Validate the copied members manifest and complete the registry's current namespace and publication process. |
| Glama repository listing | [Listing](https://glama.ai/mcp/servers/marino129/creationloop-mcp) has an obsolete banner but still carries marketing copy and old tools. | Refresh after the corrected source is reviewed and published; verify the resulting page. |
| Glama hosted mirror | [Mirror](https://glama.ai/mcp/connectors/ai.creationloop/creationloop) represents the retired registry identity. | Check how the current members identity is represented after registry publication. |
| MCP.so | [Listing](https://mcp.so/servers/creationloop-mcp) still advertises `/api/mcp`, the old four tools and design-partner signup. Its stdio label conflicts with the remote configuration. | Correct endpoint, transport, purpose, tools and onboarding links. |
| Cline Marketplace | [Issue 1981](https://github.com/cline/mcp-marketplace/issues/1981) was withdrawn by the publisher and closed October 28. The comment defers a separate `/claim/mcp` submission until more clients are tested. | Complete current client evidence, then prepare the new member discovery submission. Do not label the old issue accepted or pending review. |
| MCPServers.org | [Listing](https://mcpservers.org/servers/marino129/creationloop-mcp) still presents the marketing offer and old four tools. | Correct the listing after the current documentation is published. |
| MCPMarket | The prior submission runbook records this destination. A current accepted listing was not established in this sweep. [Site](https://mcpmarket.com/) | Find and verify any existing entry before editing or making a duplicate submission. |
| ChatGPT | No public Bureau directory listing was observed in this sweep. A custom connection is a separate path. [Custom connection guide](https://developers.openai.com/plugins/deploy/connect-chatgpt) | Prepare the discovery and evidence scope below, run client checks, then follow the current submission process. |
| Claude | No public Bureau directory listing was observed in this sweep. [Submission guidance](https://claude.com/docs/connectors/building/submission) distinguishes Community listing from Verified status. | Test the current remote connector and prepare the supported listing path. Do not claim Verified status. |
| LobeHub | A current CreationLoop listing was not established in this sweep. [Directory](https://lobehub.com/mcp) | Verify coverage and its current submission path before adding it to active distribution work. |

Additional destinations need current route checks. [PulseMCP](https://www.pulsemcp.com/servers)
reports new submissions and edits paused. [Smithery's update](https://www.smithery.ai/future)
states that connection management ended October 31 while the directory remains.
Neither is evidence of a current CreationLoop listing.

## ChatGPT submission preparation

This section constrains the planned public ChatGPT submission. It does not
describe a restriction already implemented on the general endpoint.

OpenAI's current [plugin guidelines](https://developers.openai.com/plugins/plugin-guidelines)
prohibit sales of digital products and services, including indirect freemium
upsells. Public metadata must describe the functionality without pricing or
promotional claims.

Prepare a ChatGPT profile for **public discovery and evidence**. Relevant free
profile onboarding may answer an explicit onboarding request; it must not
become an unrelated call to action or a route to promote a digital purchase.
Keep paid message and job handoffs, checkout, custom-offer sales and upgrade
promotions out of the submitted experience.

The existing general endpoint includes member payment terms, `start_message`
and, when configured, `start_job`. A documentation note does not filter those
tools or their results. Verify the actual submitted tool surface and responses
against the guidelines before submission. This draft does not implement a
ChatGPT-specific tool profile or establish its acceptance.

The [submission process](https://developers.openai.com/plugins/deploy/submission)
requires a prepared plugin package, automated checks and review. Approval and
publication are separate steps. A custom connection or an entry in the MCP
Registry does not automatically list the product in ChatGPT.

## Listing copy for review

**Name:** CreationLoop

**Description:** Find public agent offerings and their providers on
CreationLoop. Read published service details and open Trust Cards to inspect
the evidence behind agent work.

**Example requests:**

- Find providers with published video production services on CreationLoop.
- Show the agents this provider lists and the people linked to them.
- Open this agent's Trust Card so I can inspect the evidence.

This copy describes discovery. It makes no claim that an agent has completed
verified work merely because a person lists it, and no claim of a public
ChatGPT or Claude listing.

## Work before submission

1. Review and publish the corrected repository documentation. Preserve the
   distinction between the retired registry identity and the members identity.
2. Check the deployed endpoint, identity, tools and profile links. Record
   source SHA and deployed release separately where release evidence exists.
3. Complete the public agent and service discovery journey in each intended
   client. Retain actual requests, results and links, plus empty-result and
   unsupported-action checks. Historical calls do not cover newly claimed tools.
4. Finish the required ChatGPT tool and response scope before preparing that
   submission. Follow each platform's current package and review requirements.
5. Prepare one record for each destination: submitted URL, endpoint, manifest
   version, timestamp, publisher, review state, live URL and last successful
   client check. Keep submitted, accepted, published and tested separate.
6. Publish or update through the destination's supported process, then inspect
   what it actually displays. Keep signup, portal and connection links aligned.

The audited static Claim connection template contains an older waitlist CTA,
while the live November 17 page uses the profile link. Reconcile the rendering
path and release evidence before carrying that source observation into a live
status claim. The complete instant onboarding journey still needs its own
end-to-end check. This listing draft changes neither the page nor the workflow.

## Existing work and historical files

- [CreationCode PR1343](https://github.com/marino129/creationcode/pull/1343)
  is an open draft for the Claim MCP guide. It is unmerged and was not
  changed by this work. Its baseline tool correction does not prove live
  client coverage or the availability of optional `start_job`.
- Public repository [PR1](https://github.com/marino129/creationloop-mcp/pull/1)
  and [PR2](https://github.com/marino129/creationloop-mcp/pull/2) concern
  the separate CreationCode runtime connector under `creationcode/`.
  They are outside the member discovery refresh.
- Root `server.json` preserves `ai.creationloop/creationloop` at `/api/mcp`.
  The new members manifest is under `members/`. Choose the intended manifest
  explicitly during registry preparation.
- Root `mcp.json` and `.cursor-plugin/plugin.json` remain private GTM review
  configuration. They must not be treated as the public Bureau installation.

## Validation of this documentation change

The draft is limited to `README.md`, `llms-install.md`, `SUBMISSIONS.md` and
`members/server.json`. Validate JSON, the source tool inventory, active setup
URLs, relative links and the absence of retired endpoints in setup commands.
Confirm the retired root manifest and private GTM configuration are unchanged.
Live MCP calls, client tests, directory edits and registry publication are
separate work and are not claimed by these documentation checks.
