# CreationCode public discovery MCP

**CreationLoop is the company. CreationCode is the current product.**

> CreationCode product information and design-partner signup. Public discovery only; no build execution.

CreationCode helps founders and small software teams scope AI software work, review a plan and maximum cost, review the result, and retain a verifiable delivery record. Earlier marketing-agent listings are outdated. This endpoint does not provision a CMO or a short-form video service.

## Two different connections

**Public discovery and signup (this repository).** Three deterministic read tools explain the current product, offer, and FAQ. One submission tool records an application with the applicant's permission. It does not create a build, authorize work, merge, deploy, or charge.

**Authenticated software delivery (separate).** Start at https://creationcode.ai/ and use the authenticated build connection configured in CreationCode. Its separate human approval gates still apply. Do not substitute this public endpoint for that connection or advertise build tools under this public listing.

## Existing connection is preserved

- Endpoint: `https://creationloop.ai/api/mcp`
- Registry identity: `ai.creationloop/creationloop` (retained for compatibility)
- Runtime name: `creationloop`
- Transport: Streamable HTTP, stateless JSON responses
- Public authentication: none
- Method: `POST` JSON-RPC 2.0; `GET` and `DELETE` return `405`
- No endpoint, registry namespace, or private GTM token rotation is part of this copy migration.

The legacy hostname is a compatibility address, not the product name. Documentation changes alone do not prove deployment; verify the live tools and product copy before treating the migration as released.

## Public tools

| Tool | Purpose and effects |
| --- | --- |
| `get_company_overview` | Read the current CreationCode overview and public-versus-build access distinction. No write or model generation. |
| `get_design_partner_offer` | Read current software design-partner terms and application expectations. No submission or authorization. |
| `get_faq` | Read current product, signup, and build-access answers. No write or model generation. |
| `submit_design_partner_application` | With applicant permission, record contact details and any message. A genuinely new signup triggers a welcome email and founder notification. No build or payment authorization. |

The submission contract is unchanged: `email` and `website` are required strings; `name`, `company`, and `message` are optional. Unknown fields are rejected. Limits remain email 3–320 characters, website 1–500, name/company up to 200 each, message up to 2000. Ask in `message`: **What are you building, and where did you find us?** Never include credentials or confidential project data.

Duplicate email addresses do not create another row or resend signup emails. A duplicate submission does not update previously stored application details. Public traffic is limited to 30 requests/minute per IP; applications have a tighter 5/minute limit.

## Source and attribution

The stored `source` remains `design-partner-mcp:{host}`, capped at 64 characters. `{host}` comes from the applicant-supplied website, with leading `www.` removed. **It is not a referring directory.** The raw website URL is not stored; name, company, and message have their existing nullable columns.

The refreshed notification includes supplied application details and the actual submission handler. Directory discovery is unknown unless separately established. Discovery details supplied in a message are self-reported; a current offer version does not prove which listing or copy the applicant saw. There is no new attribution database migration in this release.

## Read-only verification

Use a client that supports remote Streamable HTTP, with the endpoint above and no public credentials. Verify `tools/list` and the three read-tool responses. Do not submit a test application to production: that stores a record and can send emails.

```sh
curl -sS https://creationloop.ai/api/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'

curl -sS https://creationloop.ai/api/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"get_company_overview","arguments":{}}}'
```

The overview should identify CreationCode, retire the old CMO service promise, and distinguish this public connector from authenticated builds. Public tool names must remain unchanged.

## Private GTM review plugin: unchanged

The existing Cursor/GrokBot plugin remains `creationloop-gtm-review`. Its protected `GTM_REVIEW_TOKEN` is injected through the client's secret configuration, never committed or pasted into chat. Valid authenticated GTM access exposes only `review_gtm_sweep`; it does not expose public signup or execution capabilities. It reviews ten researched prospects and cannot approve or send outreach. Do not replace the private plugin configuration with a public signup configuration.

## Listing maintenance

See `SUBMISSIONS.md` for the existing-listing migration and release gates, and `llms-install.md` for agent installation boundaries. The repository name and logo remain stable; signed agent history and receipts are not rebranded.

## License

Repository documentation and configuration are MIT licensed. See `LICENSE`.
