# eccofs-model-currents-repo

The ECCOFS **vector** fields — the expensive half of the model. A sibling data repository: its own Pages site, its own cron,
its own gigabyte, holding no code of its own.

**Built 2026-09-27, published but not drawn** on the website's map (the
owner's call). `PLAN.md` is the founding plan and record; `CLAUDE.md` carries
what must not be got wrong and the shared doc doctrine.

## What it publishes

Two roots, each a vector pair on one regional grid at 0.04 degree (1647 x
1422, `regional: true`, integers at `unitScale` 0.001), the 3-hourly frame
at or before now:

| root | quantity | size |
| --- | --- | --- |
| `cur-eccofs.json` | surface currents | 21.7 MB |
| `cur-eccofs-50m.json` | currents at 50 m | 21.8 MB |

The fetcher is the site's `scripts/fetch-eccofs.py`, shared with the
sibling repository and scoped here with `--only=`.

## Storage

About 42 MB a tree (measured 2026-09-27).

## Why it is separate from `eccofs-model-fields-repo`

**Every model splits two ways along the axis that costs bytes** (decided
2026-08-30): a currents repository for the tiled vector fields, which are
expensive, and a fields repository for the scalars, which are cheap. ESPC's
tile tier is 89% of its repository's bytes — two forecast leads across five
depths — against 44-58 MB for a 2-D scalar field. Splitting gives each half
its own gigabyte.

## How it will run

The orchestrator (the site's private `pipeline/`, since 2026-09-26), the
fetchers and the published-file contract all come from
`oceansensing.github.io`, checked out at run time. This repository carries `pipeline/products.toml` and its publish workflow
(`.github/workflows/publish.yml`), and nothing else executable. **The
workflow is dispatch-only until its first dispatched run publishes**; its
three-hourly schedule is written there, commented out.

## Structure

```
PLAN.md         the founding plan and running record
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml
.github/        the publish workflow
```
