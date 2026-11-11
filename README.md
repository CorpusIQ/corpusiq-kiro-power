# CorpusIQ power for Kiro

Makes Kiro answer business questions from the systems that already hold the numbers, instead of estimating them.

Ask "how did margin move last month" or "which channel drove the most new customers" and the answer is assembled from your own accounting, CRM, ecommerce, advertising and analytics accounts, with the source named for every figure. If a source is not connected, the power tells you which one is missing rather than producing a plausible number.

## What is in the power

| Path | Purpose |
|---|---|
| `plugin.json` | Agent Plugins manifest, including the keywords that activate the power |
| `mcp.json` | Remote CorpusIQ MCP server (streamable HTTP) |
| `skills/corpusiq-truth-layer/` | The rule set the agent follows before it states any business number |

## Sources it can read

Stripe, QuickBooks, Shopify, HubSpot, GA4, Google Search Console, Google Ads, Meta Ads, Klaviyo, Mailchimp, Airtable, Notion, Slack and 40+ other business systems. Each source is authorised separately by the account owner.

## Requirements

1. A CorpusIQ account: https://www.corpusiq.io (30-day trial, no credit card required).
2. At least one connected data source. Retrieval from external systems is read-only, and customer data is not stored.
3. A Kiro install that can load remote MCP servers.

## Install

Add the power by repository URL in Kiro (**Powers** panel, then **Add Custom Power**, then **Import power from GitHub**):

```
https://github.com/CorpusIQ/corpusiq-kiro-power
```

The first tool call opens the CorpusIQ sign-in so the account owner authorises the connection.

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
