# CreationLoop MCP Server

**CreationLoop is your Marketing Agent.**

> Verified agent output. The recursive loop that gets better, and proves it.

This is the public listing for CreationLoop's remote MCP server. The server lets
any MCP-capable agent read CreationLoop's canonical company information and submit
a design-partner application on a user's behalf. It is a hosted, remote server:
there is nothing to install and no key to configure. Point your client at the
endpoint below and connect.

- **Endpoint:** `https://creationloop.ai/api/mcp`
- **Transport:** Streamable HTTP (stateless, JSON responses)
- **Authentication:** none required
- **Method:** `POST` only (JSON-RPC 2.0)

---

## What the server is

CreationLoop is a Marketing Agent for early-stage founders and small brands. The
MCP server exposes a small, deterministic surface: three read tools that return
CreationLoop's canonical public copy verbatim, and one write tool that submits a
design-partner application. No model sits in the response path of the read tools,
so their output is fixed text, not generated on the fly.

The server is remote and hosted by CreationLoop. Your client connects over
Streamable HTTP; there is no local process, no package to install, and no
credential to supply.

---

## Transport details

The server implements the MCP Streamable HTTP transport in **stateless** mode:

- **URL:** `https://creationloop.ai/api/mcp`
- **Accepted method:** `POST` with a JSON-RPC 2.0 body.
- **Response mode:** plain JSON (`application/json`). The server runs with JSON
  responses enabled and no SSE stream, so each request gets a single JSON reply.
- **Sessions:** none. Every request builds a fresh server and transport pair, so
  there is no session id to track and no session to resume or delete.
- **`GET` and `DELETE`:** return HTTP `405` with a JSON-RPC error
  (`code -32000`, message "Method not allowed. POST JSON-RPC to this endpoint.").
  Because the server is stateless there is no SSE stream to open on `GET` and no
  session to remove on `DELETE`.
- **Server identity:** name `creationloop`, version `0.1.0`.

### Rate limits

Limits are per client IP, on a fixed 60 second window:

- **All MCP traffic:** up to 30 requests per minute. Over the limit, the server
  replies with HTTP `429` and a JSON-RPC error (`code -32000`, message
  "Too many requests. Try again shortly.").
- **`submit_design_partner_application`:** a tighter 5 submissions per minute.
  Over the limit, the tool returns a tool result flagged as an error with the
  text "Too many requests. Try again shortly." (the JSON-RPC call itself
  succeeds; the error is carried in the tool result).

---

## Tool reference

The server exposes four tools.

### `get_company_overview`

- **Input:** none. Schema is an object with no properties (`additionalProperties: false`).
- **Output:** a single text block. What CreationLoop is, how the content loop
  works, the two run modes, proof, philosophy, and the pricing stance, served
  verbatim from CreationLoop's canonical site copy.

### `get_design_partner_offer`

- **Input:** none. Schema is an object with no properties (`additionalProperties: false`).
- **Output:** a single text block describing the design-partner program: what
  partners get, what CreationLoop asks in return, and how to apply. Served
  verbatim from the canonical site copy.

### `get_faq`

- **Input:** none. Schema is an object with no properties (`additionalProperties: false`).
- **Output:** a single text block of frequently asked questions and answers,
  served verbatim from the canonical site copy.

### `submit_design_partner_application`

Submits an application to CreationLoop's design-partner program. The founder
reviews every application and follows up by email.

**Input schema** (strict; unknown fields are rejected):

| Field     | Type   | Required | Constraints            | Server field description (verbatim)                                  |
|-----------|--------|----------|------------------------|----------------------------------------------------------------------|
| `email`   | string | yes      | valid email, 3 to 320 chars | "Applicant email address (required)."                            |
| `website` | string | yes      | 1 to 500 chars         | "The brand's website URL (required)."                                |
| `name`    | string | no       | up to 200 chars        | "Applicant name (optional)."                                         |
| `company` | string | no       | up to 200 chars        | "Company name (optional)."                                           |
| `message` | string | no       | up to 2000 chars       | "What should your CMO know? Context for the email follow-up (optional)." |

> The field descriptions above are the server's own text, reproduced verbatim
> so agents match the deployed contract exactly.

**Output:** a text confirmation. On success the message confirms the application
was received for the brand's host and states that the founder reviews every
application and follows up at the email provided. On invalid input the tool
returns an error result naming the validation problem.

**What is stored.** A successful submission records a lead row with:

- the **email**, normalized (trimmed and lowercased);
- a **source** string of the form `design-partner-mcp:{host}`, where `{host}` is
  the hostname derived from the `website` value (leading `www.` stripped), with
  the whole source string capped at 64 characters;
- the **name**, **company**, and **message** you provide, each trimmed to its
  content or stored as null when blank or absent;
- a server-assigned id and a creation timestamp.

**What is not stored.** The raw `website` URL is not persisted; only the derived
hostname survives, inside the `source` string. The requester's IP address is used
only for in-memory rate limiting and is not written to storage.

**Idempotency and email.** Submissions are idempotent on the email address: a
duplicate email does not create a second row. Welcome and internal notification
emails are sent only for a genuinely new signup. If persistence fails, the tool
returns an error asking the applicant to email the founder directly instead.

---

## Connect

The server is a remote Streamable HTTP MCP server with no authentication. Use the
config block for your client.

### Claude Code

Add the server from the command line:

```sh
claude mcp add --transport http creationloop https://creationloop.ai/api/mcp
```

### Claude Desktop

Claude Desktop connects to remote Streamable HTTP servers through the `mcp-remote`
bridge. Add this to your `claude_desktop_config.json`:

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

If your version of Claude Desktop supports custom remote connectors directly, you
can instead add the endpoint URL `https://creationloop.ai/api/mcp` as a custom
connector with no authentication.

### Cursor

Add this to your Cursor MCP config (`~/.cursor/mcp.json` for a global entry, or
`.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "creationloop": {
      "url": "https://creationloop.ai/api/mcp"
    }
  }
}
```

---

## Verify the connection

Once connected, ask your client to list tools. You should see
`get_company_overview`, `get_design_partner_offer`, `get_faq`, and
`submit_design_partner_application`. A raw check with `curl`:

```sh
curl -sS https://creationloop.ai/api/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

---

## License

The contents of this listing repository (documentation and configuration) are
released under the MIT License. See [LICENSE](./LICENSE).
