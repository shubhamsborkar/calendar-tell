---
name: calendar-tell
description: >-
  Read how a public company is BEHAVING after earnings — confident or scared — and
  where that posture disagrees with the street. Four fixed moves on one ticker: (1)
  the investor-event calendar in the ~6 weeks after the latest earnings date, (2)
  the same window across the prior five quarters to set the company's own normal,
  (3) guidance vs. actual delivery, and (4) the analyst picture — buy/hold/sell
  counts and average target vs. current price. Sources every figure; names
  undisclosed items. Confident-or-scared read ONLY — no buy/sell/hold call. Use
  whenever the user names a ticker and asks how it is "acting" or "behaving" after
  a quarter — "confident or scared," "gone quiet," "keep their word on guidance" —
  or wants the calendar + guidance + analyst read together, even without saying
  "calendar tell." Apt after a guidance cut, miss, or leadership change. NOT for:
  "why is X down" selloff/sector work, earnings-update reports, initiating
  coverage, one-number lookups, or buy/sell/price-target requests.
---

# Calendar Tell

## The thesis you are testing

Companies that feel good about a quarter put themselves in front of investors —
they fill the calendar with conference appearances, fireside chats, analyst days.
Companies that feel bad go quiet and do the legal minimum. The way management
*behaves* after a print often says more than the print itself, because behavior is
harder to spin than a press release.

Your job is to run four fixed moves on one ticker, tie every number to a public
source, and end with a plain-English read: **is this company acting confident or
acting scared, and where does its behavior disagree with what the street believes?**

You give **no buy/sell/hold advice and no price prediction.** You are reading
posture, not making a trade.

## Input

A single ticker (e.g. `LULU`). If the user hasn't said which quarter, anchor on the
**most recent reported quarter** and work backwards. Confirm the company's fiscal
calendar early — many retailers/consumer names have fiscal years that end in
Jan/Feb, so "Q1 FY2026" may report in June. Getting the earnings dates right is the
backbone of moves 1–3.

## Data sources and tools

Use whatever is connected, in this order of preference, and **cite the public URL
for every number you report**:

- **A financial-data MCP (e.g. FMP / Financial Modeling Prep)** if available — best
  for exact earnings dates, reported revenue/EPS, analyst rating counts, price
  targets, and the current price. If it requires authentication, ask the user to
  run `/mcp` and authenticate, then proceed; don't block the whole task waiting.
- **Company IR site and press-release archive** (e.g. `corporate.<company>.com` /
  `investor.<company>.com`) — the primary source for earnings dates, guidance
  ranges, and the "Events & Presentations" calendar. The quarterly results press
  releases contain the explicit guidance ranges verbatim — quote them, don't
  paraphrase.
- **Newswires and filings** — Business Wire / PR Newswire / GlobeNewswire,
  SEC 8-K exhibits, the definitive proxy (for the annual meeting date).
- **Earnings-call transcripts** — Motley Fool, Seeking Alpha, Investing.com — for
  management's exact words and tone.
- **Analyst aggregators** — stockanalysis.com, MarketBeat, TipRanks, Benzinga —
  for rating counts, average price target, and current price when no financial MCP
  is connected.

Run independent lookups in parallel where you can — the four moves don't depend on
each other, so fan them out rather than doing them in series.

### Sourcing discipline (this is the point of the skill)

- **Every figure gets a public source link**, inline, next to the number or in the
  row it sits in. A reader should be able to click and verify.
- **If something isn't disclosed, say "not disclosed" — never guess or back-fill.**
  A genuinely quiet calendar window or an undisclosed guidance figure is a finding,
  not a gap to paper over.
- **When aggregators disagree** (they often do on average price targets, especially
  right after a guidance change because some figures are stale), report the range
  and the disagreement rather than picking one silently. Flag figures that look
  pre-cut/stale.
- Distinguish **"confirmed/occurred"** from **"scheduled/announced"** for events,
  and **"reported actual"** from **"guided"** for financials.

## The four moves

Run all four, every time, in this order. Keep the structure identical run-to-run so
results are comparable across companies.

### Move 1 — The post-earnings calendar (the latest window)

Find the most recent earnings date. Define the window as that date through **~6
weeks after it** (the 4–6 week window; use 42 calendar days as the standard so it's
consistent). List **every investor event** on the calendar in that window:

- the earnings call itself,
- broker/bank conference appearances (Goldman, Morgan Stanley, William Blair, ICR,
  Piper Sandler, JPMorgan, Jefferies, Oppenheimer, Bernstein, etc.),
- investor/analyst days, fireside chats, webcasts,
- the annual stockholder meeting if it falls in-window,
- the next scheduled earnings date if it lands in-window.

Give each event a name, date, type, status (confirmed vs scheduled), and a source
URL. If the window is empty apart from the earnings call, **say so explicitly.**

### Move 2 — The calendar against the last five quarters (the company's own normal)

Repeat Move 1's window for the **previous four quarters** as well, so you have the
same ~6-week post-earnings window for **five quarters total**. Build one tally table:
quarter, earnings date, event count in window, and what the events were. Cite the
earnings date and every event.

**Interpret the count against the company's own baseline, not an absolute scale.**
This is the single most important nuance: some companies *never* press-release
conference appearances, so their baseline is one event (the call) every quarter. For
those companies a raw count tells you little — what matters is:

- **Voluntary vs. mandatory.** The earnings call, the annual meeting, and recurring
  rituals (e.g. an annual ICR appearance every January) are *calendar-mandated or
  habitual* — they are **not** confidence signals. Strip them out mentally.
- **Incremental outreach during stress is the real tell.** A confident turnaround
  team facing a beaten-down stock usually *adds* something — an analyst day, a
  special investor update, an extra conference swing — to sell the recovery story.
  The **absence** of any incremental, voluntary outreach during a crisis is itself
  the signal, even if the headline event count looks "normal" or even "busy"
  because an annual meeting happened to fall in the window.
- Be honest about traceability: if the company doesn't press-release conferences,
  quiet undisclosed appearances can't be ruled out — say so.

### Move 3 — Guidance versus the delivery track record

Read the latest earnings release/call and capture **exactly** what management guided:

- next-quarter revenue and EPS ranges, and
- full-year revenue and EPS ranges, and whether the full-year guide was
  **raised / cut / maintained** versus the prior quarter's full-year guide.

Then build the track record over the same five quarters. For each quarter, score the
**actual reported result against the company's OWN prior guide** — did revenue and
EPS land **above the top end / inside the range / below the floor**? Also trace the
**full-year guide trajectory** quarter by quarter (the sequence of raises and cuts).

Two patterns to surface explicitly, because they're what "keeps its word" actually
means:

- **Near-term guide vs. actuals:** a company that beats its own next-quarter guide
  every time is *sandbagging* — setting a low bar it clears. Note the hit rate
  (e.g. "beat its own EPS guide 5 of 5 quarters").
- **Full-year guide trajectory:** a company can beat every near-term guide while
  *repeatedly cutting the full year*. That combination — "beats the bar it sets,
  keeps lowering the bar" — is the honest read of credibility. Trust the short-term
  guide; treat the full-year guide as the thing that's been moving.

Quote the ranges verbatim with sources. If a quarter's guidance figure wasn't
disclosed, say so rather than estimating.

### Move 4 — The analyst picture

Report, as of a stated date and with sources:

- **current stock price** (and the date/close it reflects),
- **rating mix:** number of Buy / Hold / Sell (note Strong Buy/Sell if broken out)
  and the consensus label,
- **average 12-month price target** and the **implied upside/downside vs. the
  current price**,
- notable **post-earnings rating/target actions** (upgrades, downgrades, target
  cuts) with the firm names.

Surface the internal contradictions, because they're where the read lives:

- when **average targets imply upside but the consensus rating is Hold/Reduce**,
  that means the street doesn't trust its own targets yet — the targets are lagging
  and probably still falling.
- when **the rating mix is Hold-heavy with a real Sell tail**, note it.

This is reporting the street's posture, **not** endorsing it. No "the stock looks
cheap/expensive," no implied recommendation.

## The read — confident or scared

Close with a plain-English synthesis. Pull the four moves together into a single
judgment and defend it with the specific behavioral tells you found. Useful tells,
in both directions:

**Scared / defensive:** cutting the full-year guide hard; guiding revenue to shrink;
**externalizing blame** (e.g. "negative media commentary," "the macro") rather than
owning execution; a **leadership vacuum** (interim/placeholder management, departed
CEO); **no incremental voluntary investor outreach** during a drawdown; going dark
on the calendar versus its own normal.

**Confident:** *adding* investor events to sell a plan; sandbagging the near-term
guide (quietly expecting to beat); raising the buyback; pointing to a real bright
spot (a segment/geography genuinely growing); maintaining or raising the full-year.

Then answer the second half directly: **where does the company's behavior disagree
with what the street believes?** Common axes:

- **Temporary vs. structural** — management frames the trouble as fixable/transitory
  while the street prices structural decline (downgrades, target cuts, segment
  guided down).
- **The street disagreeing with itself** — targets say upside, ratings say don't buy.
- **The quarter vs. the year** — a likely near-term guide beat sitting under a cut
  full-year outlook and an impaired story.

End on the one-line posture: confident, scared, or (most often) a specific blend —
e.g. "near-term execution still credible, but the story has broken, run by a
caretaker team doing the public minimum."

**No buy/sell/hold recommendation, no price call.** If the user pushes for one,
restate that this skill reads posture only and point them to the sourced facts.

## Output template

Produce a Markdown report with this exact skeleton so runs are comparable:

```markdown
# <COMPANY> (<TICKER>) — Post-<Quarter> Behavioral Read

**Anchor facts:** earnings date, what was reported, current price (with date),
leadership situation. [sources]

## 1. The post-earnings investor calendar — and the company's own normal
<Move 1 events for the latest window + Move 2 five-quarter tally table, with the
voluntary-vs-mandatory interpretation. Source every date and event.>

## 2. What management guided — and whether they keep their word
<Latest next-quarter and full-year guidance (verbatim ranges), then the five-quarter
actual-vs-own-guide track record and the full-year guide trajectory. [sources]>

## 3. The analyst picture (as of <date>)
<Current price, Buy/Hold/Sell counts, average target + implied move, recent actions,
the internal contradictions. [sources]>

## 4. Plain-English read: confident or scared?
<The synthesis: the posture judgment defended by specific tells, then where the
company's behavior disagrees with the street. No buy/sell advice.>

---
*Generated <date>. Every figure cited to a public source inline. <Note any data feed
that was unavailable and what was used instead. Name anything not disclosed.>*
```

If the user asks you to save it, write it as a Markdown file where they specify
(otherwise just deliver it inline).

## Guardrails

- **No investment advice.** No buy/sell/hold, no "fairly valued," no price target of
  your own, no implied "this is a good entry." You read behavior; you don't trade.
- **Cite or say "not disclosed."** Never present an unsourced number as fact, and
  never invent an event, a guidance figure, or an analyst count to fill a gap.
- **Run all four moves, every time**, in the same structure, so two companies (or
  two quarters of the same company) can be compared apples-to-apples.
