# The Calendar Tell

A confident company fills its investor calendar after a good quarter and goes quiet after a bad one.

This repo documents, end to end, how I read a company's post-earnings behavior with one plain-English paragraph in Claude Code, using Lululemon (LULU) as the live case in the days after it cut guidance. It accompanies this edition of Alpha with AI:(https://ai.shikshannivesh.com/p/i-taught-ai-to-read-a-companys-earnings)]

## What is in here

* **process/** — the chats, start to finish. `01-the-run.md` is the one paragraph I typed and the full output it produced: one prompt ran all four moves, and this is the part that matters — the method transfers to any ticker this repo has never heard of. `02-building-the-skill.md` is the follow-up session that turned that read into a reusable skill and stress-tested it on other tickers, so you can see how it was built and validated, not just the finished file.
* **outputs/** — the read, split by move: the five-quarter calendar count, guidance versus delivery, the analyst picture, and the verdict. Every figure traces to a public source.
* **data/** — the provenance file documenting where every number came from. No price CSVs were scraped; this run is built from company filings, releases, transcripts, and labeled aggregators.
* **skill/** — the reusable skill that was left over after the read was done. Not the other way around.

## The prompt that started it

You do not need the skill to use the idea. Paste this into Claude Code, Claude Cowork, or any AI you use, swap the ticker:

```
Look at [TICKER]. It just reported. I want to know how the company is behaving
after this quarter, because companies that feel good fill their investor calendar
and companies that don't go quiet. First, list every investor event on its IR
calendar in the four to six weeks after the earnings date. Then do the same for
the last four or five quarters so I can see whether this quarter is busier or
quieter than the company's own normal. Next, read the latest earnings call: what
did management guide for next quarter and the full year, and how does that compare
to what they guided and then delivered over recent quarters? Finally, pull the
analyst picture, buys/holds/sells and the average target versus price. Cite a
public source for every number, and if anything isn't disclosed, say so. End with
a plain read: confident or scared, and where its behavior disagrees with the street.
```

## Install the skill

Copy the `skill/calendar-tell/` folder into `~/.claude/skills/`, or use the packaged `calendar-tell.skill` file. Then, in Claude Code:

```
calendar-tell LULU
```

That one line is the whole prompt — or just ask in plain English ("is LULU acting confident or scared after earnings?"); the skill triggers on the intent, not a magic word. It runs all four moves, cites a public source for every number, and reports confident-or-scared with no buy/sell call.

## The honest caveat

This is a tell, not a verdict machine. The first time it ran on a real company it corrected me: the raw event count said confident, the real read said scared, and the gap between those two is the whole skill. Read the four moves together, never one alone. It builds the picture in minutes instead of an afternoon. You still decide.

## Disclaimer

Educational and research purposes only. Nothing here is investment advice or a recommendation. See 00-disclaimer.md.
