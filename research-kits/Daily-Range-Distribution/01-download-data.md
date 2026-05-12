# Step 1 — Download the Data from TradingView

This step gets you a CSV file containing daily OHLC plus the three computed columns the study needs: **Range**, **Average Bar Range**, and **Range / ABR**.

You'll need to have the indicator installed first. If you haven't, do [step 2](./02-install-indicator.md) before this.

---

## Setup

Open the chart of your instrument in TradingView.

**Use the continuous futures contract**, not the front month. On TradingView these are usually labelled with a `1!` suffix (e.g. `FDAX1!`, `ES1!`, `NK1!`, `HSI1!`). The continuous contract gives you the longest history without contract-roll gaps.

For cash instruments or individual stocks, just use the normal symbol.

---

## Set the timeframe

Switch the chart to the **daily timeframe (1D)**.

This is the only timeframe the study expects. Do not export weekly or 4-hour data — the bin widths and the "ABR" definition assume daily bars.

---

## Use the 24-hour session

If you're on a futures chart, TradingView lets you choose between "Regular Trading Hours" (the cash session of the underlying market) and "Electronic Trading Hours" or the full 24-hour session.

**Use the 24-hour session** (sometimes labelled "ETH" or just "24h"). The study profiles the entire trading day, not just the cash session.

You can usually toggle this in the chart's bottom bar — there's a small clock icon that opens session settings. Pick the option that says 24 hours, or the one without "RTH" or "Regular" in the name.

---

## Set the time zone

Open the chart settings → Symbol → Time Zone (or click the clock at the very bottom right of the chart).

Set the time zone to **the exchange's local time zone**:

| Instrument | Time zone |
|---|---|
| ES, NQ, RTY, YM (CME) | America/Chicago |
| FDAX (EUREX) | Europe/Berlin |
| HSI (HKEx) | Asia/Hong_Kong |
| Nikkei (CME or OSE) | Asia/Tokyo |
| FTSE 100 | Europe/London |
| Gold, Oil (NYMEX/COMEX) | America/New_York |

The time zone choice doesn't change the OHLC numbers (a daily bar is a daily bar), but it makes the date column line up with how traders actually talk about the market. A Monday on a Tokyo chart in Tokyo time is a Monday on the calendar — set to UTC, half the bars look like Sunday.

---

## Apply the indicator

If you haven't already, paste the indicator from [step 2](./02-install-indicator.md) into the Pine Editor, save it, and click **Add to chart**.

Open the **Data Window** panel on the right side of the chart. You should see three new entries:

- Range
- Average Bar Range
- Range / ABR

If you see them, the indicator is working.

---

## Export the CSV

Click the **little down-arrow at the top of the chart** (or right-click on the chart background) → **Export chart data**.

A dialog opens. Settings to use:

- **Time format:** ISO (so timestamps come out as `2024-01-15` rather than fractional weirdness)
- **Include hidden indicators:** off (irrelevant — there are no hidden ones for this)
- **All exporters:** export everything available

Click **Export**.

A CSV file downloads. Open it briefly to sanity-check:

- There should be columns for `time`, `open`, `high`, `low`, `close`, plus `Range`, `Average Bar Range`, `Range / ABR`
- The first 7 rows will have a blank "Average Bar Range" (the moving average needs 8 bars to start) — this is expected
- You should have several years of history — ideally 10+ years, but even 3-4 years gives a usable distribution

Save the CSV somewhere you can find it. The filename TradingView gives it (e.g. `EUREX_FDAX1!_1D_xxxxx.csv`) is fine — no need to rename.

---

## Common gotchas

**Only a few hundred rows in the export.** TradingView shows fewer historical bars on shorter timeframes by default. Scroll the chart to the very far left before exporting to force it to load older bars. Alternatively, on TradingView the keyboard shortcut **Alt + S** (or Cmd + S on Mac) jumps to the oldest available bar.

**No "Range / ABR" column in the export.** The indicator wasn't actually added to the chart, or you exported before applying it. Confirm the Data Window shows the three values, then re-export.

**A whole column of blank "Average Bar Range" values.** The indicator's ABR Length input is set higher than the number of bars available. Either lower the length (default 8 is fine for almost any instrument) or get more history.

**Date column shows times like "03:00:00".** Your time zone is set wrong, or the export captured timestamps from the session open. Daily bars don't have a meaningful time-of-day — only the date portion matters. You can ignore the time, or strip it out in the AI step.

---

Once you have the CSV, go to [step 3 — run the study](./03-run-the-study.md).
