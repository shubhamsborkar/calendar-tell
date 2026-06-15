# 02 — Building the Skill

After the LULU run, the next request was to make the process reusable. This file
documents how the `calendar-tell` skill was drafted, tested, and packaged — so you
can see how it was built and validated, not just the finished file (which lives in
[`../skill/`](../skill/)).

## The prompt, exactly as typed

```text
Turn this into a reusable skill called calendar-tell that takes a single ticker and runs all four moves the same way every time: the post-earnings calendar, that calendar against the last five quarters, guidance versus the delivery track record, and the analyst picture. Cite a public source for every number. Give no buy or sell advice, just the confident-or-scared read.
```

## Step 1 — Draft the skill

The skill-creator workflow was used. Because the LULU conversation already *was* the
worked example, the intent was captured directly from it rather than re-interviewed.
A single `SKILL.md` was written that encodes the four fixed moves plus the
analytical nuances the LULU run had surfaced:

- **Move 1 + 2 (calendar):** interpret event counts against the company's *own*
  normal; strip out mandatory/habitual events (earnings call, annual meeting,
  recurring conferences like ICR); treat *absence of incremental outreach during a
  drawdown* as the real tell rather than the raw count.
- **Move 3 (guidance):** score actuals against the company's *own* prior guide and
  trace the full-year guide trajectory; surface the "beats the bar it sets, keeps
  lowering the bar" pattern.
- **Move 4 (analysts):** buy/hold/sell counts and average target vs. current price;
  flag the "targets imply upside but rating says Hold" contradiction.
- **Guardrails:** a public source for every number or an explicit "not disclosed";
  **no buy/sell/hold advice — confident-or-scared read only.**

## Step 2 — Design the eval

The user chose a **full eval loop**: run the skill against fresh, recently-reported
tickers, each **with the skill** and **without it (baseline)**, then compare. Three
tickers were chosen to exercise different postures:

| Eval | Ticker | Why |
|---|---|---|
| 0 | **NKE** (Nike) | guidance withdrawn / beaten-down → the "scared" case |
| 1 | **TGT** (Target) | turnaround quarter, guide raised, *natural phrasing that never names the skill* → tests triggering + the "confident" case |
| 2 | **COST** (Costco) | healthy grower that gives *no guidance by policy* → edge case |

The exact eval prompts used:

```text
[eval 0 — NKE]
Nike (NKE) just reported earnings. I want to understand how the company is behaving afterward — is it acting confident or scared? Look at how busy its investor calendar is in the weeks after this quarter versus its own normal over the last several quarters, what management guided versus what they've actually delivered, and the current analyst picture. Cite a public source for every number, and don't give me a buy or sell call — just the read.

[eval 1 — TGT]
How's Target's management acting after this last quarter — confident, or have they gone quiet? Ticker TGT. Pull the investor events on their calendar after earnings, check whether they keep their word on guidance, and give me the analyst consensus and price target versus where it trades. Source everything please.

[eval 2 — COST]
Costco (COST) reported recently. Walk me through their post-earnings investor calendar, their guidance versus what they actually delivered, and the analyst picture, and tell me whether they're behaving like a confident company or a scared one.
```

## Step 3 — Run all six (with-skill + baseline), grade, benchmark

All six runs executed as parallel research sub-agents. Each produced a full sourced
report. They were then graded against nine structural assertions (does it run all
four moves, establish a 4+ quarter baseline, distinguish mandatory vs. voluntary
events, score guidance vs. the company's own guide, report the rating mix + target
vs. price, source every number, end with a confident-or-scared verdict, withhold
buy/sell advice, and name where behavior disagrees with the street).

**Result — pass rate, timing, tokens (3 runs each config):**

| Metric | With skill | Baseline (no skill) | Delta |
|---|---|---|---|
| Pass rate (9 assertions) | 100% (9/9 all three) | 100% (9/9 all three) | **+0.00** |
| Avg time | ~386 s | ~252 s | +134 s |
| Avg tokens | ~65.9k | ~45.7k | +20k |

Per-run timing/tokens captured during the loop:

| Run | Time | Tokens |
|---|---|---|
| NKE with-skill | 386.6 s | 64,635 |
| NKE baseline | 288.2 s | 48,997 |
| TGT with-skill | 383.4 s | 63,899 |
| TGT baseline | 188.4 s | 31,924 |
| COST with-skill | 387.4 s | 69,200 |
| COST baseline | 278.1 s | 56,174 |

A standalone HTML review viewer (Outputs + Benchmark tabs) was generated so the
outputs could be compared side by side.

### Honest reading of the benchmark

The **+0.00 delta is the finding, not a failure.** The eval prompts already
enumerate the four moves, so a capable model reproduces the structure with or
without the skill — the structural checks could not *discriminate*. The skill's real
value lives where these prompts didn't apply pressure:

1. **Triggering** on vague asks ("is TGT acting scared?") where the user does *not*
   spell out the moves — a description-quality question, not a structural one.
2. **The subtler interpretation rules** (voluntary-vs-mandatory events, the
   full-year guide trajectory, the street-disagreement angle), which a coarse
   keyword grader can't measure for quality. Qualitatively the with-skill runs were
   more disciplined here — e.g. on Costco the with-skill run explicitly flagged that
   the company issues no guidance *by policy* and scored against consensus instead.

A useful incidental signal: the **Target baseline** run (no skill) spontaneously
noted that a purpose-built `calendar-tell` skill exists for exactly this task —
evidence the niche is real and discoverable.

## Step 4 — Triggering optimization (attempted; two environment blockers)

The plan was to run the automated description-optimizer (20 realistic
should-trigger / should-not-trigger queries, scored 3× each over up to 5
iterations). It **could not complete in this environment**, for two concrete
reasons — both recorded here rather than papered over:

1. **The rewrite step needs a raw `ANTHROPIC_API_KEY`.** It calls the Anthropic SDK
   directly; this OAuth session did not expose an API key, so the loop crashed at
   the point where it would have proposed a better description.
2. **The eval step's trigger scores were unreliable.** Every should-trigger query
   scored `0/3` — including `"do the calendar tell thing on PTON"`, which names the
   skill outright. A description cannot be why an explicit-name request fails to
   fire; that is the headless test harness not detecting skill invocation, not a
   real signal. The one trustworthy part: the **negatives all behaved correctly**
   (selloff-triage, earnings-report, initiate-coverage, calendar-app, and buy/sell
   queries stayed off).

Raw scoring line from the run, for transparency:

```text
Train: 18/36 correct, precision=100% recall=0% accuracy=50%
  [FAIL] expected=True:  lulu just cut guidance again. is management acting confident...
  [FAIL] expected=True:  how is NKE behaving after earnings? feels like they've gone quiet
  [PASS] expected=False: why is LULU down 60% over the past year? is this idiosyncratic...
  [PASS] expected=False: build me a full earnings update report on AAPL fiscal Q2 ...
  [PASS] expected=False: initiate coverage on TGT — full institutional initiation report...
```

### Manual description hardening (what was actually done instead)

Rather than tune against a broken meter, the description was hardened by hand using
the one trustworthy signal (the negatives) and standard practice:

- front-loaded the trigger phrasings ("acting/behaving after a quarter," "confident
  or scared," "gone quiet," "keep their word on guidance"), and
- added an explicit **`NOT for:`** boundary fencing the skill off from its real
  siblings in the environment — `stock-selloff-triage` ("why is X down"),
  `earnings-analysis` (earnings-update reports), and `initiating-coverage` — plus
  one-number lookups, calendar-app scheduling, and any buy/sell/price-target
  request.

The 20-query trigger set used for the attempt is preserved alongside the workspace
for reference. *(This was not a clean automated optimization; it is labeled as a
manual edit.)*

## Step 5 — Package

The skill was validated and packaged. One fix was required along the way: the first
packaging attempt failed validation because the hardened description exceeded the
**1024-character** frontmatter limit (it was ~1676 chars), so it was trimmed to
~1019 characters while keeping the front-loaded triggers and the `NOT for:`
boundaries. It then validated and packaged cleanly.

Both artifacts are included in this repo under [`../skill/`](../skill/):

- [`../skill/calendar-tell/`](../skill/calendar-tell/) — the full skill folder
  (`SKILL.md` + `evals/`), copied from `~/.claude/skills/calendar-tell/`.
- [`../skill/calendar-tell.skill`](../skill/calendar-tell.skill) — the packaged,
  installable file.
