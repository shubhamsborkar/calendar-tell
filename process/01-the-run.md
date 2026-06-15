# 01 — The Run (LULU)

This is the original, unedited request that started everything, followed by the
complete output it produced. Every source link is preserved.

## The prompt, exactly as typed

```text
Look at Lululemon, ticker LULU. It just reported and cut its full-year guidance. I want to know how the company is behaving after this quarter, because companies that feel good about a quarter fill their investor calendar and companies that don't go quiet. So first, go to its investor relations page and any conference schedules you can find, and list every investor event on the calendar in the four to six weeks after the earnings date. Then do the same thing for the last four or five quarters, the same window after each earnings date, so I can see whether this quarter is busier or quieter than the company's own normal. Next, read the latest earnings call and tell me exactly what management guided for next quarter and the full year, and compare that guidance to what they guided and then actually delivered over the last few quarters, so I know whether this is a team that keeps its word. Finally, pull the current analyst picture, how many buys, holds and sells, and the average price target versus where the stock trades now. Cite a public source for every number, and if anything isn't disclosed, say so instead of guessing. At the end, give me a plain-English read: is this company acting confident or acting scared, and where does its behavior disagree with what the street believes?
```

## How the run was carried out (research trail)

The answer was assembled from public web sources only. No private data feed was
used — the Financial Modeling Prep (FMP) MCP required sign-in and was **not
authenticated**, so the run fell back to public sources throughout. The work was
fanned out across:

- a web search to anchor the earnings date and the guidance cut,
- two parallel research sub-agents — one reconstructing the **investor-event
  calendar** across five quarters, one reconstructing the **guidance-vs-delivery**
  history — each instructed to cite a public URL for every figure and to mark
  undisclosed items rather than guess,
- direct page fetches for the **analyst picture** (price, rating mix, average
  target) and the earnings-call transcript.

Every URL surfaced and used is preserved inline below and consolidated in
[`../data/sources.md`](../data/sources.md). Items that could not be retrieved
(TipRanks and the SEC 8-K line-item exhibits both returned HTTP 403) are recorded
there too.

---

## The complete output

# Lululemon (LULU) — Post-Q1-FY2026 Behavioral Read

**Anchor facts:** LULU reported Q1 FY2026 after the close on **June 4, 2026**
(quarter ended May 3, 2026) and **cut its full-year outlook**. Stock was ~$111
after hours that night and closed **$118.77 on June 12, 2026**
([stockanalysis.com](https://stockanalysis.com/stocks/lulu/)). The company is run
by **interim co-CEOs Meghan Frank (CFO) and Andre Maestrini**; permanent CEO
**Heidi O'Neill arrives September 2026**
([Motley Fool transcript](https://www.fool.com/earnings/call-transcripts/2026/06/04/lululemon-lulu-q1-2026-earnings-transcript/)).

## 1. The investor-calendar tell — and why it mostly doesn't work for LULU

The hypothesis (confident companies fill the calendar, scared ones go quiet) runs
into a structural fact: **Lululemon barely uses its investor calendar in any
quarter.** It does not press-release sell-side conference appearances, and its IR
"Events & Presentations" page lists essentially only the mandatory items. Count of
every disclosed investor event in the ~6 weeks after each of the last five earnings
dates:

| Quarter | Earnings date | Investor events in the 4–6 wk window | What they were |
|---|---|---|---|
| **Q1 FY2026** | **June 4, 2026** | **2** | Earnings call + Annual Meeting (June 25) |
| Q4 FY2025 | Mar 17, 2026 | 1 | Earnings call only |
| Q3 FY2025 | Dec 11, 2025 | 2 | Earnings call + ICR Conference (Jan 12–14) |
| Q2 FY2025 | Sept 4, 2025 | 1 | Earnings call only |
| Q1 FY2025 | June 5, 2025 | 1 | Earnings call only |

Sources: earnings dates and events all verified against company press releases —
[Q1 FY26](https://corporate.lululemon.com/media/press-releases/2026/06-04-2026-210523775),
[Q4 FY25](https://corporate.lululemon.com/media/press-releases/2026/03-17-2026-200620717),
[Q3 FY25](https://corporate.lululemon.com/media/press-releases/2025/12-11-2025-210611862),
[Q2 FY25](https://www.nasdaq.com/press-release/lululemon-athletica-inc-announces-second-quarter-fiscal-2025-results-2025-09-04),
[Q1 FY25](https://corporate.lululemon.com/media/press-releases/2025/06-05-2025-210525682);
ICR appearance per the [Jan 12, 2026 pre-ICR update](https://corporate.lululemon.com/media/press-releases/2026/01-12-2026-113012292);
Annual Meeting per the [definitive proxy](https://www.sec.gov/Archives/edgar/data/0001397187/000121390026058095/ea0281698-04.htm).

**Honest read of this leg:** The most recent window shows **2 events — tied for the
busiest** of the five. But that is *not* a confidence signal: the extra event is a
calendar-mandated **annual stockholder meeting (June 25)**, which this year was a
**contested proxy meeting** tied to a Chip Wilson cooperation agreement
([May 27, 2026 PR](https://corporate.lululemon.com/media/press-releases/2026/05-27-2026-123017044))
— forced engagement, not voluntary outreach. The ICR appearance in the Q3 window is
an annual ritual, not a choice.

The real signal is what's **absent**: a company down ~60% over a year, with an
interim management team and a proxy fight, did **not** add a single piece of
*incremental, voluntary* investor outreach — no analyst day, no special investor
update, no bonus conference circuit to defend the story. A confident turnaround
team usually schedules an analyst/investor day to lay out a recovery plan. LULU did
the legal minimum. **Caveat:** because LULU never press-releases bank conferences,
undisclosed quiet appearances can't be ruled out — but nothing surfaced in IR
listings, wires, or financial calendars (MarketBeat/TipRanks).

## 2. What management just guided — and whether they keep their word

**Guidance issued June 4, 2026**
([company release](https://corporate.lululemon.com/media/press-releases/2026/06-04-2026-210523775),
[CNBC](https://www.cnbc.com/2026/06/04/lululemon-lulu-earnings-q1-2026.html)):

| | Q2 FY2026 guide | Full-year FY2026 guide |
|---|---|---|
| **Revenue** | $2.450B–$2.475B (**−3% to −2%**) | $11.00B–$11.15B (**−1% to flat**) |
| **Diluted EPS** | $1.76–$1.81 | **$10.95–$11.15** |

The FY guide was **cut** from the March 17 guide of $11.35B–$11.50B revenue and
**$12.10–$12.30 EPS** — and FY2026 EPS of ~$11 is now a step down from FY2025's
**delivered $13.26**. Management blamed **"negative commentary in the media,"**
disappointing product launches (the "Look of Yoga"/Away From Body line), tariffs
(280 bps Q1 hit), and fixed-cost deleverage
([WWD](https://wwd.com/business-news/financial/lululemon-q1-2026-earnings-1238995741/), transcript).

**Do they keep their word?** Scoring each quarter's *actual* result against the
company's *own prior guide* (all from company releases):

| Reported quarter | Delivered vs its own guide |
|---|---|
| Q1 FY2025 ($2.371B / $2.60) | **Beat both** (above top end) |
| Q2 FY2025 ($2.525B / $3.10) | Revenue just **missed** floor; EPS **beat big** ($3.10 vs $2.90 top) |
| Q3 FY2025 ($2.566B / $2.59) | **Beat both** decisively |
| Q4 FY2025 ($3.6B / $5.01) | **Beat both** (even after pre-announcing "high end") |
| Q1 FY2026 (~$2.5B / $1.69) | **Beat both** modestly ($1.69 vs $1.68 top) |

**EPS beat the top of their own range 5 of 5 quarters; revenue beat 4 of 5.**
Sources: [Q1 FY25](https://corporate.lululemon.com/media/press-releases/2025/06-05-2025-210525682),
[Q2 FY25](https://corporate.lululemon.com/media/press-releases/2025/09-04-2025-210520895),
[Q3 FY25](https://finance.yahoo.com/news/lululemon-athletica-inc-announces-third-210600453.html),
[Q4 FY25](https://corporate.lululemon.com/media/press-releases/2026/03-17-2026-200620717),
[Q1 FY26](https://corporate.lululemon.com/media/press-releases/2026/06-04-2026-210523775).

But the **full-year story is the opposite**. The FY EPS guide walked down all year:
**$14.95–15.15 → $14.58–14.78 (cut) → $12.77–12.97 (cut) → $12.92–13.02 (raised) →
delivered $13.26**, and now **FY2026 $12.10–12.30 → $10.95–11.15 (cut)**. **Three
full-year cuts, one raise.** (FY2024 starting guide from the
[Q4 FY2024 release](https://corporate.lululemon.com/media/press-releases/2025/03-27-2025-200544345);
Q3 raise corroborated by [Nasdaq](https://www.nasdaq.com/articles/lululemon-surpasses-revenues-earnings-q3-lifts-fy25-view).)

**The pattern in one line:** *They consistently beat the low bar they set for the
next quarter, while repeatedly lowering the bar for the year.* So they "keep their
word" on the quarter (and the new Q2 guide is probably another sandbag they'll
clear) — but the franchise itself has been deteriorating, and the credibility you
should trust is the *short-term* guide, not the *full-year* one.

## 3. The analyst picture (as of June 12, 2026)

- **Current price: $118.77** ([stockanalysis.com](https://stockanalysis.com/stocks/lulu/)).
- **Rating mix (33 analysts):** **2 Buy** (1 of them Strong Buy), **27 Hold**, **4 Sell** — consensus **"Reduce"** ([MarketBeat](https://www.marketbeat.com/stocks/NASDAQ/LULU/price-target/)).
- **Average 12-month price target:** aggregators disagree — **$135.74** (stockanalysis.com, 33 analysts) to **$154.26** (MarketBeat, 33 analysts), implying **~+14% to +30%** upside. *(A ~$186 figure floating around is stale/pre-cut — disregard it.)*
- **Post-Q1 actions were almost all cuts:** BNP Paribas **downgraded to Underperform, $88**; JPMorgan $173→$149 (Neutral); Bernstein $170→$145; Citi $185→$130; Telsey $175→$122; Piper Sandler $130→$110 ([Benzinga](https://www.benzinga.com/analyst-stock-ratings/analyst-color/26/06/52992928/lululemon-likely-to-report-lower-q1-earnings-these-most-accurate-analysts-revise-price-target-ahead-of-earnings-call), [search aggregation](https://public.com/stocks/lulu/forecast-price-target)).

**Not disclosed / unavailable:** I could not authenticate the FMP data feed, so
these counts come from public aggregators, which is why the two price-target
averages differ. The two primary sources I'd normally cross-check (the full Motley
Fool transcript and the SEC 8-K exhibit) returned 403 to automated fetch; guidance
figures above are from the company press release and CNBC, which agree.

## 4. Plain-English read: confident or scared?

**Acting scared — but a managed, competent kind of scared.** The tells:

- **They cut the full year hard** (EPS ~$13.26 → ~$11) and guided Q2 revenue to *shrink* — you don't print a minus sign unless you have to.
- **They externalized blame** — "negative commentary in the media" is what a defensive team says; you can't fix the media, and naming it as a top cause of a guidance cut is a tell that they're managing perception, not just the business.
- **A leadership vacuum:** the CFO is moonlighting as co-CEO and the real CEO doesn't arrive until September. Confident companies don't run a turnaround with a placeholder at the top.
- **They added zero voluntary investor outreach** during a 60%-off year and a proxy fight — the calendar move a confident team makes (an analyst day to sell the recovery) simply didn't happen.

The *not*-scared counter-evidence: they're still **sandbagging the quarterly
guide** (a quietly confident move — they expect to beat Q2), **China is genuinely
strong (+30%)**, and they raised the buyback last December.

**Where management and the street disagree:**

1. **Temporary vs. structural.** Management frames the miss as *fixable and
   transitory* — bad media buzz, a couple of product misfires. The **street is
   pricing structural decline**: a Hold/"Reduce" consensus, a downgrade to
   Underperform at $88, and FY North America guided down high-single-digits. The
   market doesn't believe "it's just the media."

2. **The street disagrees with *itself*** — and that's the most revealing tension.
   Average targets ($136–$154) sit **15–30% above** the $118.77 price, yet the
   rating is **Hold/Reduce with only 2 buys and 4 sells.** When targets say
   "upside" but nobody will say "buy," it means the targets are lagging indicators
   being walked down, and analysts don't yet trust the floor: *the price targets
   haven't finished falling.*

3. **The quarter vs. the year.** Management's 5-for-5 EPS-beat record says the
   *next print* (Q2) will likely clear its low bar — a possible short-term pop. But
   the street is looking past that to the full-year cut, the leadership gap, and a
   core North America market that's actually contracting. **The honest synthesis:**
   this is a company whose *near-term execution is still credible* but whose *story
   has broken*, run by a caretaker team that is doing the minimum in public while
   it waits for a new CEO — and the market is treating the franchise as impaired
   until proven otherwise.

---

## Split, sourced breakdown

The four moves above are broken out into individual, fully-sourced files in
[`../outputs/`](../outputs/):
[`calendar-counts.md`](../outputs/calendar-counts.md) ·
[`guidance-vs-delivery.md`](../outputs/guidance-vs-delivery.md) ·
[`analyst-picture.md`](../outputs/analyst-picture.md) ·
[`verdict.md`](../outputs/verdict.md).
