# eccofs-model-currents-repo — the founding plan and running record

The ECCOFS **vector** fields — the expensive half of the model. Started 2026-08-30, when the repository was created. **Nothing
is built.**

## What it is for

`u`, `v`, `ubar`, `vbar` from ECCOFS, regridded and rotated. **No
product is defined yet.**

Nothing is built. The measured study behind ECCOFS lives in
`oceansensing.github.io/PLAN.md` under "Queued: ECCOFS" (2026-08-05) and is
deliberately not copied.

## Why it is its own repository

**Every model splits two ways** (decided 2026-08-30, `espc-model-repo`'s
`DECISIONS.md` D2): `<model>-model-currents-repo` for the tiled vector fields
and `<model>-model-fields-repo` for the scalars. The axis is what costs bytes,
measured rather than chosen — ESPC's tile tier is **89% of its repository**,
two leads across five depths, against 44-58 MB for a 2-D scalar field.

**`espc-model-repo` is the one exception to the naming**, kept knowingly: it
is the ESPC currents repository, and its URL is a live origin that a rename
would 404. Read it as `espc-model-currents-repo`.

## Storage

Unmeasured. At 3 km over Grand Banks to the Orinoco this is the first
repository where the **grid itself** may be the constraint rather than the
tile tier.

## Open

1. Everything. No product is defined and nothing is wired.
2. `pipeline/products.toml`, which must declare only roots the site's
   `test-schema.mjs --roots` publishes.
3. Its cron, offset from the siblings so two repositories never read the same
   upstream in the same minute.
