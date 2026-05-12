# Step 1 — Download the Data from TradingView

This step gets you a CSV file containing daily OHLC plus the three computed columns the study needs: **Range**, **Average Bar Range**, and **Range / ABR**.

You'll need to have the indicator installed first. If you haven't, do [step 2](./02-install-indicator.md) before this.

---

## Setup

Open the chart of your instrument in TradingView.

**Use the continuous futures contract**, not the front month. On TradingView these are usually labelled with a `1!` suffix (e.g. `FDAX1!`, `ES1!`, `NK1!`, `HSI1!`). The continuous contract gives you the longest history without contract-roll gaps.

In the symbol settings (gear icon → Symbol tab), make sure **"Adjust data for contract changes"** is enabled. This back-adjusts the price series so contract-roll gaps don't appear as fake daily ranges. Without this, you'll get a handful of rollover days with artificially large Range values.

For cash instruments or individual stocks, just use the normal symbol — no contract-roll setting needed.

---

## Set the timeframe

Switch it to the **24-hour timeframe (24hr)** instead of daily timeframe.

---

## Set the time zone

Click on the **time displayed at the bottom right of the chart** (just under the price axis). A list of time zones opens. Pick the exchange's local time zone:

| Instrument | Time zone |
|---|---|
| ES, NQ, RTY, YM (CME) | UTC-6 (Chicago / America/Chicago) |
| FDAX (EUREX) | UTC+1 (Berlin / Europe/Berlin) |
| HSI (HKEx) | UTC+8 (Hong Kong / Asia/Hong_Kong) |
| Nikkei (CME or OSE) | UTC+9 (Tokyo / Asia/Tokyo) |
| FTSE 100 | UTC+0 (London / Europe/London) |
| Gold, Oil (NYMEX/COMEX) | UTC-5 (New York / America/New_York) |

The time zone choice doesn't change OHLC values, but it makes the date column line up with how the market actually trades. Set wrong, you can get a Monday on the chart showing up as Sunday in your CSV.

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
- **All exporters:** export everything available

Click **Export**.

A CSV file downloads. Open it briefly to sanity-check:

- There should be columns for `time`, `open`, `high`, `low`, `close`, plus `Range`, `Average Bar Range`, `Range / ABR`
- The first 7 rows will have a blank "Average Bar Range" (the moving average needs 8 bars to start) — this is expected
- You should have several years of history — ideally 10+ years, but even 3-4 years gives a usable distribution

Save the CSV somewhere you can find it. The filename TradingView gives it (e.g. `EUREX_FDAX1!_1D_xxxxx.csv`) is fine — no need to rename.

---

Once you have the CSV, go to [step 3 — run the study](./03-run-the-study.md).
