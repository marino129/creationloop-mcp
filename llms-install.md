# Install the CreationCode public discovery MCP

CreationLoop is the company; CreationCode is the current product. This repository describes public product-information and design-partner signup tools. It is not the authenticated software build connector and does not provision a CMO.

Use the existing remote Streamable HTTP endpoint `https://creationloop.ai/api/mcp`. Public information and signup require no authentication. Preserve existing client connections, server identity `creationloop`, and registry identity `ai.creationloop/creationloop`.

For clients whose remote MCP configuration supports `url`:

```json
{
  "mcpServers": {
    "creationloop": {
      "url": "https://creationloop.ai/api/mcp"
    }
  }
}
```

Use the client's own supported remote-connector configuration rather than installing an unrelated local server. List tools and read `get_company_overview`, `get_design_partner_offer`, or `get_faq` to verify the live copy. Read tools are deterministic and do not submit applications or start builds.

Do not call `submit_design_partner_application` as a connectivity test. It records a contact and sends emails for new signups. Call it only with the applicant's explicit permission. Required inputs are `email` and `website`; optional inputs are `name`, `company`, and `message`. Unknown fields are rejected. Use the message for the intended software work and where the applicant found the listing, without inventing a discovery source or including secrets.

The source suffix is the applicant's website hostname, not a referral. Duplicate emails are a no-op and do not update stored details.

For software builds, open https://creationcode.ai/ and follow the authenticated connection configured there. Never infer a build endpoint, reuse someone else's approval, or treat a signup as authorization to build or spend.

The separate private `creationloop-gtm-review` plugin retains its protected token configuration and review-only authority. Do not overwrite it with the public configuration above.
