# Eval Validation — how the skill was stress-tested

This folder is the raw evidence behind the validation summarized in
[`../02-building-the-skill.md`](../02-building-the-skill.md). After the
`calendar-tell` skill was drafted, it was run against three fresh, recently-reported
tickers — each **with the skill** and **without it (a no-skill baseline)** — so the
two could be compared directly.

The three were chosen to exercise different post-earnings postures:

| Ticker | Why it was chosen |
|---|---|
| **Nike (NKE)** | guidance withdrawn / beaten-down → the "scared" case |
| **Target (TGT)** | turnaround quarter, guide raised; prompt phrased *naturally, never naming the skill* → tests triggering + the "confident" case |
| **Costco (COST)** | healthy grower that issues **no guidance by policy** → edge case |

## What's in here

- **`nike/`, `target/`, `costco/`** — each has `with-skill.md` (the report produced
  with `calendar-tell`) and `baseline.md` (the same prompt with no skill).
- **`benchmark.md`** — the quantitative comparison (pass rate, time, tokens) and how
  to read the +0.00 delta.
- **`review.html`** — the standalone side-by-side viewer (the file that opened in a
  browser during the session). Download it and open it locally; it has an "Outputs"
  tab to click through each ticker and a "Benchmark" tab. It is a generated
  artifact — the markdown files above contain the same content in a
  repo-friendly form.

## Important caveats for readers

- These are **June 2026 point-in-time snapshots** for **test tickers** — they exist
  to show how the *skill* behaves, not as current research on NKE, TGT, or COST.
  The same **educational-only, not-investment-advice** terms apply; see
  [`../../00-disclaimer.md`](../../00-disclaimer.md).
- Two of the six reports (Nike `baseline.md` and Target `with-skill.md`) were saved
  from the run's text output after a file-write hiccup during the session; their
  content is exactly as produced, just persisted by hand.
- Figures in these reports are sourced inline by the runs themselves; they were not
  re-verified to the standard of the main LULU run in [`../../outputs/`](../../outputs/).
