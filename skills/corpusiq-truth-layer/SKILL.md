---
name: corpusiq-truth-layer
description: Answer business questions from connected sources with a citation on every number, and name the missing connector instead of estimating. Use for revenue, margin, churn, CAC, pipeline, traffic or any question about a specific company's own numbers.
---

# CorpusIQ truth layer

## When this applies

The question is about a specific business's own numbers: revenue, margin, churn, retention, CAC, runway, pipeline, orders, traffic, spend. Public data cannot answer it. Only the company's accounts can.

## Step 1: Identify the metric, then the source

State the metric in one line and name the system that owns it.

- Revenue, invoices, bills, margin: accounting (QuickBooks, Xero)
- Payments, subscriptions, churn, MRR: billing (Stripe)
- Orders, AOV, product mix: store (Shopify)
- Pipeline, deals, win rate: CRM (HubSpot, Salesforce)
- Sessions, conversions, channels: analytics (GA4)
- Queries, impressions, rankings: search (Search Console)
- Spend, ROAS, CPA: advertising (Google Ads, Meta Ads)

If two systems own the same word, say which definition you are using before you answer. Revenue in a billing system and revenue in an accounting system are not the same measure.

## Step 2: Call the connector

Use the CorpusIQ MCP tools. Prefer `ask_corpusiq` for a whole-business question, because it selects a fixed, read-only runbook and validates the prerequisites before it runs.

## Step 3: Cite every figure

Each number carries its source and its period. For example: "Gross margin 61.4% for October, from QuickBooks, invoices posted through 31 October." A number with no source is not an answer.

## Step 4: Name the hole

If the required source is not connected, stop. Say which connector is missing and what it would unlock. Do not substitute an estimate, an industry benchmark, or a figure from a different period.

Say: "Churn needs Stripe connected. Once it is connected this answer takes one query."

## Step 5: Report the definition

Close with the definitions used, the period covered, and anything excluded. This is what makes two reports comparable a month apart.

## Never

- Never estimate a company's own metric.
- Never present a benchmark as the company's number.
- Never mix periods without saying so.
- Never write a figure into a document without its source.
