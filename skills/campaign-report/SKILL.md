---
name: campaign-report
description: Use when the user asks how an email campaign, broadcast, newsletter or journey performed, wants to compare several sends, asks why a broadcast has not gone out, or wants a chart of email or web push results from their Spreeflo workspace.
---

# Report on campaign performance

Explicit instructions from the user take priority over this skill. Everything here only reads, except `render_chart`, which saves a chart file in the workspace.

## Input

What to report on: a named campaign or broadcast, "the last newsletter", a journey, or a set to compare. If the request does not identify one, find candidates and ask.

## Steps

1. **Find the campaign.**
   - One-off campaigns and broadcasts: `list_campaigns` (newest first; optionally `contactListId`). "The last newsletter" is the newest one that has been sent.
   - Always-on automations (welcome, re-engagement): `list_journeys`.
   - If several match the user's words, list them by name and date and ask which.
2. **Read the results.**
   - Email: `get_campaign_performance` with its `campaignId`. It returns totals and a per-email breakdown with rates already computed.
   - Web push: `get_webpush_performance`.
   - A broadcast that has not sent, or its settings: `get_broadcast`, which lists what blocks sending right now.
3. **Report** in a short summary, then the numbers:
   - sent, delivered or bounced, open rate, click rate, replies and complaints;
   - for a campaign with several emails, which email did best and worst;
   - revenue only when `hasRevenueData` is true, in the currency the result gives.
4. **Chart** when it helps: comparing several campaigns, or emails within one. Call `render_chart` with a complete Vega-Lite spec whose rows are inline in `data.values`, already aggregated. Cite the url it returns.
5. **Comparing** campaigns: call the performance tool once per campaign, up to about five, and put them side by side.

## Rules

- Use the rates the tools return. Do not recompute them another way.
- Do not quote industry benchmarks or averages; compare only with the workspace's own campaigns.
- If a campaign has not been sent yet, say so instead of reporting zeros as results.
- Do not suggest sending or scheduling from here. Those happen in the Spreeflo app.
