# CorpusIQ for AI agents: Kiro power, Claude Code and Cursor plugin

Makes an AI client answer business questions from the systems that already hold the numbers, instead of estimating them.

Ask "how did margin move last month" or "which channel drove the most new customers" and the answer is assembled from your own accounting, CRM, ecommerce, advertising and analytics accounts, with the source named for every figure. If a source is not connected, the agent tells you which one is missing rather than producing a plausible number.

## What is in this repository

| Path | Purpose |
|---|---|
| `plugin.json` | Agent Plugins manifest (open standard), including the keywords that activate the power |
| `mcp.json` | Remote CorpusIQ MCP server declaration for Agent Plugins clients |
| `.claude-plugin/plugin.json` | Claude Code and Cursor plugin manifest |
| `.claude-plugin/marketplace.json` | Marketplace index, so the plugin installs by name |
| `skills/corpusiq-truth-layer/` | The rule set the agent follows before it states any business number |
| `llms-install.md` | Complete install path written for agents that set servers up by reading a repository |
| `logo-400.png` | 400x400 listing mark |

## Sources it can read

Stripe, QuickBooks, Shopify, HubSpot, GA4, Google Search Console, Google Ads, Meta Ads, Klaviyo, Mailchimp, Airtable, Notion, Slack and 40+ other business systems. Each source is authorised separately by the account owner. Retrieval is read-only.

## Requirements

1. A CorpusIQ account: https://www.corpusiq.io (30-day trial, no credit card required).
2. At least one connected data source.
3. A client that can load remote MCP servers over Streamable HTTP.

## Install

### Kiro

Add the power by repository URL (**Powers** panel, then **Add Custom Power**, then **Import power from GitHub**):

```
https://github.com/CorpusIQ/corpusiq-kiro-power
```

### Claude Code

```
claude plugin marketplace add CorpusIQ/corpusiq-kiro-power
claude plugin install corpusiq@corpusiq-marketplace
```

### Cursor

Add the server directly to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "corpusiq": {
      "url": "https://mcp2.corpusiq.io/mcp"
    }
  }
}
```

### Cline and other clients that read a repository

Follow `llms-install.md`. It carries the settings for Cline, Claude Desktop, VS Code and any generic remote MCP client, plus the handshake check and the responses that look like failures but are not.

The first tool call opens the CorpusIQ sign-in so the account owner authorises the connection. There is no API key to paste.

## Ground rule

Every number must come from a connected source and carry a citation, or be labelled as unknown. A report with a named hole in it is worth more than one with an invented metric.

## Links

- Product: https://www.corpusiq.io
- MCP setup: https://www.corpusiq.io/mcp
- Documentation: https://docs.corpusiq.io
- Privacy policy: https://www.corpusiq.io/privacy
- Terms: https://www.corpusiq.io/terms
- Support: media@corpusiq.io

MIT licensed. Built by CorpusIQ.
