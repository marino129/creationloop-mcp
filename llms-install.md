# CreationLoop MCP: Agent Install Guide

This file is written for an AI agent (such as Cline) setting up the CreationLoop
MCP server on a user's behalf. Follow these steps exactly.

## What this server is

CreationLoop is a Marketing Agent. This is a **remote** MCP server hosted by
CreationLoop. There is nothing to clone, build, or install locally, and there is
no API key, token, or environment variable to set. You only add a remote server
entry pointing at the public endpoint.

- **Endpoint:** `https://creationloop.ai/api/mcp`
- **Transport:** Streamable HTTP (stateless, JSON responses)
- **Authentication:** none

## Install steps

1. **Do not** run any install, build, or clone command. This server is remote.
2. Add a new MCP server entry to the user's MCP settings file. Use the key
   `creationloop` and the remote endpoint URL. The shape is:

   ```json
   {
     "mcpServers": {
       "creationloop": {
         "url": "https://creationloop.ai/api/mcp"
       }
     }
   }
   ```

3. If the client only supports launching a local command and cannot dial a remote
   URL directly, bridge to it with `mcp-remote`:

   ```json
   {
     "mcpServers": {
       "creationloop": {
         "command": "npx",
         "args": ["-y", "mcp-remote", "https://creationloop.ai/api/mcp"]
       }
     }
   }
   ```

4. Save the settings file and reload the MCP servers.

## Verify

List the server's tools. You should see exactly four:

- `get_company_overview`
- `get_design_partner_offer`
- `get_faq`
- `submit_design_partner_application`

Call `get_company_overview` with empty arguments (`{}`). A successful response is
a text block describing CreationLoop. That confirms the server is connected.

## Tool notes for the agent

- The three `get_*` tools take **no arguments**. Pass an empty object.
- `submit_design_partner_application` requires `email` and `website`. `name`,
  `company`, and `message` are optional. Unknown fields are rejected. Only submit
  it when the user has clearly asked to apply to the design-partner program, and
  confirm the email address with the user first.
- No tool requires or accepts credentials.

## Troubleshooting

- **`405 Method not allowed`:** the client sent a `GET` or `DELETE`. This server
  accepts `POST` JSON-RPC only. Use a client that speaks the MCP Streamable HTTP
  transport over `POST`.
- **`429 Too many requests`:** you exceeded the per-IP rate limit (30 requests per
  minute overall, 5 per minute for application submissions). Wait and retry.
