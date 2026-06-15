# Benchmark — calendar-tell skill validation

**Date:** June 15, 2026 · **Model:** Claude Opus 4.8 (the session model; the
research sub-agents inherited it) · **Setup:** 3 evals (NKE, TGT, COST), **1 run
each per configuration** — i.e. 3 with-skill runs and 3 baseline (no-skill) runs,
six in total.

Each run was graded against the same **9 structural assertions** (runs all four
moves; establishes a 4+ quarter calendar baseline; distinguishes mandatory vs.
voluntary events; scores guidance vs. the company's own guide; reports the rating
mix + target vs. price; sources every number; ends with a confident-or-scared
verdict; withholds buy/sell advice; names where behavior disagrees with the street).

## Summary

| Metric | With skill | Baseline (no skill) | Delta |
|--------|------------|---------------------|-------|
| Pass rate (9 assertions) | 100% ± 0% | 100% ± 0% | **+0.00** |
| Time | 385.8s ± 2.1s | 251.6s ± 54.9s | +134.2s |
| Tokens | 65,911 ± 2,872 | 45,698 ± 12,457 | +20,213 |

## How to read the +0.00 delta (it is the finding, not a failure)

The eval prompts themselves already enumerate the four moves, so a capable model
reproduces the structure **with or without** the skill — the structural checks
can't *discriminate* between the two. The skill's real value lives where these
prompts didn't apply pressure:

1. **Triggering** on vague asks ("is TGT acting scared?") where the user does *not*
   spell out the moves — a description-quality question, not a structural one.
2. **The subtler interpretation rules** (voluntary-vs-mandatory events, the
   full-year guide trajectory, the street-disagreement angle), which a coarse
   keyword grader can't measure for quality. Qualitatively the with-skill runs were
   more disciplined here — e.g. on Costco the with-skill run explicitly flagged that
   the company issues **no guidance by policy** and scored against consensus
   instead.

A useful incidental signal: the **Target baseline** run (no skill) spontaneously
noted that a purpose-built `calendar-tell` skill exists for exactly this task —
evidence the niche is real and discoverable.

*The reports these numbers grade are in `nike/`, `target/`, and `costco/`
(`with-skill.md` vs. `baseline.md` in each). The side-by-side viewer is
`review.html`.*
