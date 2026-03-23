# Benchmark 2030 Dashboards

## Overview

This directory contains the dashboard generation infrastructure for Benchmark 2030 metrics visualization. Dashboards provide at-a-glance status of all key metrics defined in `benchmark-2030/targets.yaml`.

## How Dashboards Are Generated

### 1. Source: targets.yaml

All dashboard metrics originate from `benchmark-2030/targets.yaml`. This file is the single source of truth for what is being measured and what the target values are. Any change to targets must be reflected in this file before dashboard generation will produce correct output.

### 2. CI Metrics Export

On each push to main, the CI pipeline exports measurable metrics to a structured log:

- **Test coverage** — extracted from Jest coverage report JSON
- **CI pass rate** — computed from GitHub Actions workflow run history via API
- **S11 violations** — count of sentinel failures in the past 30 days (target: 0)
- **npm package count** — queried from the npm registry for `@silence/*` packages

These measurements are written to `.benchmark-metrics-latest.json` (git-ignored) for local inspection and optionally to a Supabase metrics table for historical trending.

### 3. Dashboard Generation Workflow

The `benchmark-dashboard.yml` workflow (planned for Q2 2026) will:

1. Read `targets.yaml` and `quarterly/*.md` reports
2. Fetch latest CI metrics from the exports above
3. Generate a `dashboard-latest.md` in this directory with current status indicators
4. Commit the updated dashboard to main with a `chore: update benchmark dashboard` commit message

### 4. Quarterly Manual Review

Automated dashboards capture quantitative metrics. Each quarterly report in `benchmark-2030/quarterly/` adds the qualitative context — what was achieved, what was missed, and why. The combination of automated metrics and human narrative provides the complete Benchmark 2030 record.

## Dashboard Format

When generated, `dashboard-latest.md` follows this format:

```markdown
# Benchmark 2030 — Dashboard
Last updated: YYYY-MM-DD

## Technical Quality
| Metric | Target | Current | Status |
|---|---|---|---|
| Test coverage | 80% | XX% | 🟡 / 🟢 |
...

## Compliance
...

## Research Output
...

## Ecosystem Growth
...
```

## Status Indicators

| Symbol | Meaning |
|---|---|
| PASS | Metric meets or exceeds target |
| WARN | Metric within 10% of target threshold |
| FAIL | Metric below threshold |
| N/A | Not yet measurable |

## Implementation Status

Dashboard automation is scheduled for Q2 2026. Manual quarterly reports are the primary tracking mechanism until automation is in place.
