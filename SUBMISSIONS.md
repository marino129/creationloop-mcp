# Submissions Runbook

A step-by-step runbook for the founder to list the CreationLoop MCP server in the
public MCP directories. Every step is manual founder execution. Nothing here is
automated, and none of it has been run.

## Before you start

Complete these prerequisites once; every directory depends on them.

1. **Create the public repository.** Push the reviewed contents of this folder to
   a public GitHub repo. Working name: `creationloop-mcp`
   (`https://github.com/marino129/creationloop-mcp`). If you use a different name
   or owner, update the `repository.url` in `server.json` and every repo link
   below to match.
2. **Add the logo.** Export `logo.png` (400x400) from `brand-mark-source.svg` per
   `LOGO_SPEC.md` and commit it to the repo root. The Cline marketplace requires
   it.
3. **Confirm the live endpoint.** From a normal network, run:
   ```sh
   curl -sS https://creationloop.ai/api/mcp \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
   ```
   The response must list `get_company_overview`, `get_design_partner_offer`,
   `get_faq`, and `submit_design_partner_application`. If it does not, stop and
   reconcile the README before submitting anywhere.
4. **Verify the schema version.** Open the `$schema` URL in `server.json` in a
   browser and confirm it resolves. The MCP registry schema is versioned by date;
   if a newer version is published, update the URL before running the registry
   publish flow.

## 1. Official MCP registry (registry.modelcontextprotocol.io)

The official registry validates `server.json` and requires you to prove ownership
of the namespace.

1. Confirm `server.json` is at the root of the public repo and validates against
   its `$schema`.
2. The server `name` is `ai.creationloop/creationloop`, which is a DNS-based
   namespace. You must prove control of `creationloop.ai`. Follow the registry's
   current publishing guide at
   `https://github.com/modelcontextprotocol/registry` (the `docs/guides/publishing`
   section) to install the `mcp-publisher` CLI.
3. Authenticate with DNS verification for `creationloop.ai`:
   ```sh
   mcp-publisher login dns --domain creationloop.ai
   ```
   Add the TXT record it prints to the `creationloop.ai` DNS zone, then complete
   the login.
4. Publish from the repo root:
   ```sh
   mcp-publisher publish
   ```
5. Confirm the entry appears via the registry API:
   ```sh
   curl -sS "https://registry.modelcontextprotocol.io/v0/servers?search=creationloop"
   ```

## 2. Cline marketplace (github.com/cline/mcp-marketplace)

Cline listings are added by opening a GitHub issue on the marketplace repo.

1. Go to `https://github.com/cline/mcp-marketplace/issues/new/choose` and pick the
   MCP server submission template.
2. Fill in the required fields:
   - **GitHub Repo URL:** `https://github.com/marino129/creationloop-mcp`
   - **Logo Image:** attach the 400x400 `logo.png`.
   - **Reason for Addition:** a short note on why the server is useful to Cline
     users. Keep it to CreationLoop's ratified public framing: CreationLoop is your
     Marketing Agent; verified agent output, the recursive loop that gets better,
     and proves it. The server lets an agent read the company overview, the
     design-partner offer, and the FAQ, and submit a design-partner application.
   - **Testing Confirmation:** before submitting, hand Cline only this repo's
     `README.md` and `llms-install.md` and confirm it connects the remote server
     and lists the four tools with no other help. Check the confirmation box.
3. Submit the issue and respond to any maintainer follow-up.

## 3. mcpmarket.com

1. Go to `https://mcpmarket.com/submit`.
2. Provide the public repo URL `https://github.com/marino129/creationloop-mcp` and,
   if asked, the remote endpoint `https://creationloop.ai/api/mcp`.
3. Fill in name (CreationLoop), the one-line description from `server.json`,
   category (marketing or similar), and upload the logo if requested.
4. Mark the transport as remote Streamable HTTP and note that no authentication is
   required.
5. Submit and wait for review.

## 4. mcp.so

1. Go to `https://mcp.so/submit` (linked as "Submit" from the mcp.so header).
2. Provide the public repo URL `https://github.com/marino129/creationloop-mcp`.
3. Fill in the name, description, and category. mcp.so reads much of the listing
   from the repo `README.md`, so make sure it is current before submitting.
4. Note the remote endpoint `https://creationloop.ai/api/mcp`, transport Streamable
   HTTP, no authentication.
5. Submit and wait for review.

## 5. mcpservers.org

1. Open `https://mcpservers.org` and find its "Add Server" or "Submit" entry
   (mcpservers.org accepts listings by pull request to its source repository).
2. Follow the site's submit link to its GitHub repo and open a pull request adding
   the CreationLoop entry: name, description, remote endpoint
   `https://creationloop.ai/api/mcp`, transport Streamable HTTP, no auth, and the
   repo link.
3. Submit the pull request and respond to review.

## After submitting

- Record each submission's URL and status somewhere durable.
- If a directory rejects or requests changes, fix the repo contents first, then
  resubmit. The public README is the source of truth every directory reads.
