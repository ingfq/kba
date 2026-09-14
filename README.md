# KBA Dashboard — overview

One HTML file that answers *how is the Kosova banking system doing, and which
bank is driving it* — from the KBA's own published PDFs, with nothing invented
in between.

## In one line

```powershell
# PDFs -> data -> audit -> index.html
```

Then open [index.html](index.html). No server, no internet, no install. Send it
as an attachment and it works on the other end.

## What it is

| | |
| --- | --- |
| **Input** | 15 KBA releases (8 quarterly, 7 monthly), 11 banks |
| **Output** | one self-contained page, ~500 KB, data inlined |
| **Charts** | 11, hand-drawn SVG, zero dependencies |
| **Guard** | 14-section data audit + 396 headless assertions |

## The four questions it answers

1. **How big is the system, and what is it made of?** Assets over time, split
   into deposits, loans, equity — with each band's share and its move on the
   prior period.
2. **Who leads, and who is moving?** League table, rank-change bump chart,
   market share, concentration (HHI / CR3 / CR5).
3. **How is a bank funded, and is it lending more than it gathers?**
   Loan-to-deposit per bank, plus each bank's *contribution* to the system
   ratio's move — so "who pushed it past 90%" has a name.
4. **Who is efficient, and why?** ROE decomposed (margin × turnover ×
   leverage), cost burden versus return, peer strips with quartiles and median.

## Principles it is built on

**Published numbers are never silently corrected.** Where KBA's printed rank
disagrees with the asset ordering, the dashboard shows the dispute rather than
picking a winner.

**Gaps are shown, not filled.** Periods without a comparable basis say so.
Mixed monthly/quarterly steps are labelled, never averaged together.

**A bad release cannot reach the page.** The audit gates the build: TOTAL
against the sum of banks, market shares to 100%, referential integrity, the
page's own printed date against the source filename. Disagreement fails the
run.

**It works on a phone.** Charts choose their layout from the width they are
handed. Filters collapse to one line plus a sheet. Every readout opens by tap,
not just by mouse.

**Nothing is drawn over anything else.** Label placement is swept across every
period × width × frequency combination and fails the build on a single overlap
or anything outside the frame.

## Adding a new release

Drop the PDF in this folder, re-run, done. Filenames carry the reporting date,
so there is no list to update. Keep the name KBA published it under.

## Where things are

| | |
| --- | --- |
| `run_kba.py` | the whole pipeline |
| `tools/kba_extract.py` | PDF → CSV (geometric parse) |
| `tools/kba_analyze.py` | ratios, growth, concentration |
| `tools/kba_audit.py` | the gate |
| `tools/index_v2.html` | the dashboard source |
| `tools/test_dashboard_v2.js` | the suite |
| `output/` | CSVs + the JSON the page inlines |


