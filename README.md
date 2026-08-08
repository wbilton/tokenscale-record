# tokenscale-record

The public, append-only verification record for **[TokenScale](https://tokenscale.dev)** —
the nightly-checked log of what 22 AI API providers published as their token prices.

## What one commit proves

Every night TokenScale's pipeline appends that day's price point for every
provider tier to `prices.json` and writes a manifest to
`verification/YYYY-MM-DD.json` saying, for each provider, whether that night's
numbers were **verified fresh** against the provider's official pricing page or
**carried forward** (`cf: true`) from the previous night without a re-check.
`promos.json` records time-limited promotional pricing windows (launch
discounts, intro pricing) with start/end dates and the official source URL for
each; the manifest lists which promos were active that night.
The commit timestamp is GitHub's, not ours. That makes each night's claim
third-party timestamped and impossible to quietly edit later.

- A night with no commit is a missed night. We do not fill gaps in afterwards.
- `night_status` is `verified` (every tier checked), `partial` (some checked),
  or `carried_forward` (no checks ran — prices copied from the night before).
- Carried nights stay carried, permanently. A later check never repaints a
  missed night. The site's [reliability page](https://tokenscale.dev/reliability)
  lists every one.

## History note (honest backfill)

The record was kept privately from **19 May 2026** to **August 2026** on the
machine that runs the nightly. `prices.json` in the first commit carries that
full history, with permanent `cf` flags marking every reconstructed
carried-forward night. Live nightly commits begin on the date of the first
commit in this repo — we did not fabricate backdated commits, because commit
dates that predate the repo are exactly the kind of theatre this record exists
to avoid.

Independent copies: the live pages are also submitted nightly to the
[Internet Archive](https://web.archive.org) (since 5 August 2026).

## Rules this repo lives by

1. Append-only. History is never rewritten and never force-pushed.
2. A failed night is a gap, not an interpolation.
3. Data only — the site's source code does not live here.

Maintained by [Bilton Projects](https://tokenscale.dev/story) · Will Bilton.
