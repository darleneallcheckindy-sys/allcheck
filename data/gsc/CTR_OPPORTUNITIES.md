# CTR Opportunities

Status: **Blocked — Needs Live GSC Export.**

This analysis requires comparing actual CTR against expected CTR for a given
position, which requires real GSC clicks/impressions/position data per
query. No live GSC data exists anywhere accessible to this session:

- No Search Console MCP connector is attached to this Claude workspace.
- No GSC export file (CSV/Sheet) was found in the connected Google Drive.
- The client's own "AllCheck SEO AEO GEO Internal Progress Tracker" lists
  this exact task ("Find high-impression, low-CTR queries/pages") as **Not
  Started**, with "Live CTR opportunity analysis pending" — confirming this
  has not been done anywhere yet, not just in this session.

## What this file will contain once GSC access exists

A table of queries where:
- impressions are meaningful (page is actually being shown),
- position is good enough to expect clicks (roughly top 10),
- but clicks/CTR are disproportionately low relative to that position.

For each, we will note whether the likely cause is a weak title, a weak meta
description, a mismatched search intent, or a SERP feature (e.g. a
featured snippet or Local Pack) absorbing clicks before checking whether a
title/meta rewrite is warranted — per the rule not to assume every low-CTR
case is a title problem.

## Action needed

- [ ] **Waiting on Client:** provide GSC access (Search Console connector for
      this workspace) or export Performance data (Query + Page + Clicks +
      Impressions + CTR + Position, last 28 days) so this file can be
      completed with real numbers.
