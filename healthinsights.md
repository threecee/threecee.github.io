---
title: HealthInsights
description: What HealthInsights does and how to use it.
---

# HealthInsights

A personal app that visualizes patterns and insights from your HealthKit
data. iPhone only. Read-only — it never writes to HealthKit.

## What it shows you

The app reads glucose readings (from your CGM), insulin doses (from your
pump or manual entries), and carbohydrate entries from HealthKit, then
surfaces patterns you'd otherwise have to spot by eye.

Three main views:

- **Insights** — the front page. Recent overnight stability, time-in-range
  for the last day/week, and the highest-priority observation right now
  (e.g., "post-dinner spikes have been larger this week").
- **Patterns** — week-over-week comparisons across times of day. Useful
  for noticing that, say, your post-breakfast control has changed since
  switching to a different breakfast.
- **IOB** — a chart of insulin-on-board over the last several hours. Use
  this to sanity-check timing of recent doses.

## Data needs

- **Glucose:** at least 24 hours of CGM readings to show anything
  useful. ~7 days for the Patterns view to detect week-over-week shifts.
- **Insulin + carbs:** as soon as they're logged in HealthKit, they
  appear in the IOB chart.

If you've just installed and granted HealthKit permissions, expect the
Insights view to be sparse for the first day or two while history
accumulates.

## Where data is processed

Aggregations and pattern detection run on a Supabase backend that Carl
operates. Your raw HealthKit data stays on your device; only summarized
queries go to the backend, and only when you have the app open. See the
[privacy policy](https://threecee.github.io/healthinsights-privacy/)
for details.

## Settings

There's a Settings tab for setting your target glucose range (default
70–180 mg/dL) and for toggling Nightscout sync if you use Nightscout
(off by default).

_Last updated: 2026-05-01_
