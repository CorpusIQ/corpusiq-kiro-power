---
title: CorpusIQ MCP install instructions for agents
description: "Install the CorpusIQ remote MCP server in Cline, Claude Code, Cursor, VS Code, Gemini CLI or any remote MCP client. One HTTP endpoint, OAuth 2.1, no package to install."
last_updated: "2026-11-11"
---
# CorpusIQ MCP: install instructions for agents

This file is written for AI agents and coding assistants (Cline, Claude Code, Cursor, VS Code, Gemini CLI, Kiro) that install MCP servers by reading a repository. It is the complete setup path. You do not need any other file.

The repository also ships an Agent Plugins manifest (`plugin.json`), an MCP server declaration (`mcp.json`) and one skill (`skills/corpusiq-truth-layer/SKILL.md`). A client that supports the Agent Plugins standard loads the server from `mcp.json` without further configuration.

## What this server is

CorpusIQ is a remote MCP server that gives an AI client read-only access to a business's own systems: QuickBooks, Shopify, Stripe, GA4, HubSpot, Klaviyo, Slack, and 40+ connectors in total. The client asks a question, CorpusIQ retrieves the records live from the connected source and returns them with the source cited. It does not retain raw customer files or full connector response payloads.

- Transport: Streamable HTTP (remote, no local install, no container, no package)
- Endpoint: `https://mcp2.corpusiq.io/mcp`
- Auth: OAuth 2.1 with dynamic client registration and PKCE
- Access: read-only retrieval. Answers cite the source system.

## Install in three steps

1. Add the remote server entry to the client config shown below, or install the plugin from this repository.
2. Start the client. It will open a browser for OAuth.
3. Sign in with a CorpusIQ account and approve. The 30-day trial needs no credit card.

There is no API key to paste and no environment variable to set. Authentication happens through the OAuth flow.

## Client configuration

### Cline

Add to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "corpusiq": {
      "type": "streamableHttp",
      "url": "https://mcp2.corpusiq.io/mcp"
    }
  }
}
```

Cline opens the browser for OAuth on first use. Approve it, then ask a business question.

### Claude Code

```bash
claude mcp add --transport http corpusiq https://mcp2.corpusiq.io/mcp
```

### Claude Desktop, and any client using `mcpServers`

```json
{
  "mcpServers": {
    "corpusiq": {
      "type": "http",
      "url": "https://mcp2.corpusiq.io/mcp"
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (global):

```json
{
  "mcpServers": {
    "corpusiq": {
      "url": "https://mcp2.corpusiq.io/mcp"
    }
  }
}
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "corpusiq": {
      "type": "http",
      "url": "https://mcp2.corpusiq.io/mcp"
    }
  }
}
```

### Generic remote MCP client

- URL: `https://mcp2.corpusiq.io/mcp`
- Transport: `streamable-http`
- Auth: OAuth 2.1, discovery at `https://mcp2.corpusiq.io/.well-known/oauth-protected-resource`
- Authorization server: `https://mcp2.corpusiq.io`
- Optional client registration endpoint: `https://mcp2.corpusiq.io/oauth/register`
- Scopes: `openid`, `email`, `profile`
- Token endpoint auth methods: `client_secret_basic`, `client_secret_post`, `none`

## Verify the installation

A correctly configured client completes this handshake. Sending `initialize` to the endpoint returns the server identity:

```bash
curl -s -X POST https://mcp2.corpusiq.io/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"install-check","version":"1.0"}}}'
```

A healthy server answers with `serverInfo.name` set to `multi-source-mcp`. After OAuth completes, `tools/list` returns the tool catalogue of 121 tools. The first tool to call for a general business question is `ask_corpusiq`.

## Expected behaviours that are not failures

- A plain `GET` to `/mcp` returns HTTP 406. That is correct. The endpoint speaks JSON-RPC over POST.
- An unauthenticated `tools/list` returns 401. That is the OAuth gate, not an outage.
- The negotiated protocol version may differ from the one requested. The server selects the version it supports.

## Frequently asked questions

### Do I need an API key or an environment variable?

No. Authentication is OAuth 2.1. The client opens a browser, the user signs in to CorpusIQ, and the client receives a token. There is no key to paste.

### Does CorpusIQ store the data it retrieves?

For MCP connector requests, CorpusIQ fetches source records live and returns them to the requesting AI client. It does not retain raw customer files or full connector response payloads, and it does not build embeddings, file indexes, or cached or indexed summaries. Query text, per-user tool-call metadata, and bounded outcome summaries are retained in operational logs for up to 30 days.

### Which tool should an agent call first?

`ask_corpusiq` for a general business question, including financial snapshots. It routes to the right connectors and returns an answer with the source cited.

## Support

- Documentation: https://docs.corpusiq.io
- Connector reference: https://www.corpusiq.io/connectors
- Connection troubleshooting: https://docs.corpusiq.io/hermes/troubleshooting/corpusiq/
