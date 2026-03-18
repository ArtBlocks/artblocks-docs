---
order: 900
description: Connect your AI agent to the Art Blocks MCP Server in under 5 minutes.
---

# Quick Start

The Art Blocks MCP Server supercharges your AI agents to become instant power users in the Art Blocks ecosystem — discovering projects, exploring portfolios, checking mint eligibility, building transactions, and scaffolding generative art scripts.

!!!contrast Connect in under 5 minutes

```
https://mcp.artblocks.io/mcp
```

[!badge variant="primary" size="l" icon="tools" text="21 tools"]  [!badge variant="success" size="l" icon="globe" text="Ethereum · Arbitrum · Base"]  [!badge variant="info" size="l" icon="shield-check" text="OAuth 2.1"]

!!!

---

## Step 1: Connect the MCP Server

Choose your client below. Each one handles OAuth automatically — you just complete a one-time browser sign-in.

==- Cursor

Add to `.cursor/mcp.json` in your project root (or `~/.cursor/mcp.json` for global access):

```json
{
  "mcpServers": {
    "artblocks-mcp": {
      "url": "https://mcp.artblocks.io/mcp"
    }
  }
}
```

Reload MCP servers via **Settings → MCP** or restart Cursor. A browser window will open for sign-in the first time a tool is invoked. After authenticating, Art Blocks tools appear in Agent mode.

==- Claude Code

Run once in your terminal:

```bash
claude mcp add --transport http artblocks-mcp https://mcp.artblocks.io/mcp
```

Then in Claude Code, run `/mcp` and choose "Authenticate" for the Art Blocks server. Complete the browser sign-in.

Optional scope flags:

```bash
claude mcp add --transport http --scope user artblocks-mcp https://mcp.artblocks.io/mcp    # global
claude mcp add --transport http --scope project artblocks-mcp https://mcp.artblocks.io/mcp  # per-project
```

==- Claude Desktop

1. Open **Settings → Connectors**
2. Click **Add connector**
3. Paste `https://mcp.artblocks.io/mcp`
4. Complete sign-in in the browser

==- ChatGPT

Requires ChatGPT Pro or Plus with Developer Mode enabled.

1. Open **Settings → Advanced → Connectors**
2. Click **Create custom connector**
3. Enter server URL: `https://mcp.artblocks.io/mcp`
4. Complete the OAuth sign-in flow

==- Windsurf

1. Open Command Palette → **"Windsurf: Configure MCP Servers"**
2. Add to `mcp_config.json`:

```json
{
  "mcpServers": {
    "artblocks-mcp": {
      "url": "https://mcp.artblocks.io/mcp"
    }
  }
}
```

3. Restart Windsurf and complete browser sign-in

==- Codex

Run once in your terminal:

```bash
codex mcp add --transport http artblocks-mcp https://mcp.artblocks.io/mcp
```

Codex will prompt you to authenticate via OAuth when a tool is first invoked.

==- :icon-terminal: Headless or custom agent?

If your agent doesn't have a browser, use the **Device Authorization flow** — see [Device flow (headless agents)](#device-flow-headless-agents) at the bottom of this page.

===

---

## Step 2: Install Agent Skills (Recommended)

[Agent Skills](https://github.com/ArtBlocks/skills) teach your AI agent Art Blocks-specific workflows and best practices — which tool to use, how to chain tools together, and how to interpret results. They activate automatically based on what you ask.

```bash
npx skills add ArtBlocks/skills
```

Install globally (available across all projects):

```bash
npx skills add ArtBlocks/skills -g
```

After installing, reload Cursor (`Cmd+Shift+P` → "Reload Window") for skills to take effect.

See the [Skills page](/mcp-server/skills/) for the full catalog and installation options.

---

## Step 3: Start Prompting

Skills activate automatically — just ask naturally:

> *"What Art Blocks projects are minting right now?"*
>
> *"Show me Tyler Hobbs' projects and the traits of Fidenza #100"*
>
> *"Help me convert my p5.js sketch to Art Blocks format"*
>
> *"Check if vitalik.eth is eligible to mint this project"*
>
> *"What does snowfro's Art Blocks portfolio look like?"*

See [Capabilities](/mcp-server/capabilities/) for the full list of tools and example questions.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| **401 Unauthorized** | Re-authenticate — your session may have expired. Restart your client or re-run the OAuth flow. |
| **Tools not appearing** | Reload MCP servers in your client settings, or restart the application. |
| **Rate limited** | Back off and retry. The server enforces per-user rate limits. |
| **OAuth popup blocked** | Allow popups for `mcp.artblocks.io` in your browser settings. |

---

## Supplementary: Authentication Reference

This section is primarily useful for agent developers debugging OAuth connections or building custom MCP clients.

### Overview

The server uses **OAuth 2.1** with [Dynamic Client Registration (RFC 7591)](https://www.rfc-editor.org/rfc/rfc7591) — no pre-registration is needed. Clients that support MCP over HTTP handle the full OAuth handshake automatically.

### Grant types

| Grant | Use case |
|-------|----------|
| **Authorization Code + PKCE** | Browser-capable clients (Cursor, Claude, ChatGPT, Windsurf) |
| **Device Authorization ([RFC 8628](https://www.rfc-editor.org/rfc/rfc8628))** | Headless agents, CLIs, relay daemons |

### Discovery endpoints

| Endpoint | URL |
|----------|-----|
| Authorization Server Metadata | `GET https://mcp.artblocks.io/.well-known/oauth-authorization-server` |
| Protected Resource Metadata | `GET https://mcp.artblocks.io/.well-known/oauth-protected-resource/mcp` |

### Device flow (headless agents)

For agents without a browser:

1. Request a device code: `POST https://mcp.artblocks.io/oauth/device/code`
2. Display the returned user code and verification URL to the operator
3. Operator visits the verification URL, enters the code, and signs in
4. Agent polls `POST https://mcp.artblocks.io/oauth/token` with `grant_type=urn:ietf:params:oauth:grant-type:device_code` until approved
5. Agent receives tokens

Both `application/x-www-form-urlencoded` and `application/json` request bodies are accepted at all OAuth endpoints.
