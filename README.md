# eccofs-model-currents-repo

The ECCOFS **vector** fields — the expensive half of the model. A sibling data repository: its own Pages site, its own cron,
its own gigabyte, holding no code of its own.

**Live since 2026-09-27, published but not drawn** on the website's map
(the owner's call). `PLAN.md` is the founding plan and record; `CLAUDE.md` carries
what must not be got wrong and the shared doc doctrine.

## What it publishes

Six roots, each a vector pair on one regional grid at 0.04 degree (1647 x
1422, `regional: true`, integers at `unitScale` 0.001). The first two are
the 3-hourly frame at or before now, from the quick-save files; the other
four, since 2026-09-28, are the daily 00 UTC snapshot at or before now, from
the history files, which hold every level:

| root | quantity | size |
| --- | --- | --- |
| `cur-eccofs.json` | surface currents | 21.7 MB |
| `cur-eccofs-50m.json` | currents at 50 m | 21.8 MB |
| `cur-eccofs-avg200m.json` | currents averaged over the top 200 m | 21.5 MB |
| `cur-eccofs-avg350m.json` | currents averaged over the top 350 m | 21.4 MB |
| `cur-eccofs-avg1000m.json` | currents averaged over the top 1000 m | 21.2 MB |
| `cur-eccofs-bottom.json` | bottom currents (the lowest s-level) | 20.7 MB |

An average's header says `depthAveraged: [0, cap]`; where the water is
shallower than the cap it is the mean of the whole column, so on the shelf
the three are one. A bottom root's header carries no depth: the lowest level
is a different depth in every cell, and the root's name says bottom.

The fetcher is the site's `scripts/fetch-eccofs.py`, shared with the
sibling repository and scoped here with `--only=`.

## Published to R2 alone (since 2026-10-10)

Declared `r2_only` in `pipeline/products.toml`: the same run builds these,
they are left out of this repository's Pages site and its status, and the R2
job publishes them beside the rest (the site pipeline's D13, its note of
2026-10-09). Their roots stay on the `published` branch, as every product's do.

| root | quantity | grid |
| --- | --- | --- |
| `uv-eccofs-<depth>m.json` | the current at each of the first 48 of Mercator's depths, 0.494 to 4833.291 m, interpolated from the model's 50 terrain-following levels below the datum, east and north as the other currents here; one root a depth named for it to the meter (`-0m` … `-4833m`), from the daily 00 UTC snapshot | 0.04 degree, `regional: true` |

## Storage

About 128 MB a tree (measured 2026-09-28; 42 MB before the history's four roots).

## Why it is separate from `eccofs-model-fields-repo`

**Every model splits two ways along the axis that costs bytes** (decided
2026-08-30): a currents repository for the tiled vector fields, which are
expensive, and a fields repository for the scalars, which are cheap. ESPC's
tile tier is 89% of its repository's bytes — two forecast leads across five
depths — against 44-58 MB for a 2-D scalar field. Splitting gives each half
its own gigabyte.

## How it runs

The orchestrator (the site's private `pipeline/`, since 2026-09-26), the
fetchers and the published-file contract all come from
`oceansensing.github.io`, checked out at run time. This repository carries `pipeline/products.toml` and its publish workflow
(`.github/workflows/publish.yml`), and nothing else executable. **Scheduled since 2026-09-27** (`43 1-23/3 * * *`), after its first dispatched run published.

## Structure

```
PLAN.md         the founding plan and running record
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml
.github/        the publish workflow
```
