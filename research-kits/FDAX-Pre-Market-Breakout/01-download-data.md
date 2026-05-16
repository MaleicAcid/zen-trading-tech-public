# Step 1 — Download the Data from TradingView

This step gets you a CSV file of 15-minute FDAX bars. The indicator reads the overnight and Frankfurt session ranges from intraday bars, so daily-bar data will not work here.

---

## The data file for FDAX

A pre-built stitched 15-minute FDAX dataset (Dec 2018 – May 2026, 153,123 bars) is included in the `data/` folder. You can use this directly with the execution prompt in step 3 without downloading anything. Skip the steps below if you are using the included data file.

---

## If you want to build your own dataset

### Symbol

Use the **continuous futures contract**: `FDAX1!` on TradingView. Do not use the front-month contract — it will have roll gaps that produce false range spikes.

### Timeframe

Set the chart to **15 minutes**.

### Session

This is the critical setting. On TradingView, set the session to **RTH only** in the chart settings. Despite the name, this gives you the continuous price series including the overnight Globex session — it is simply what TradingView calls the setting that makes the overnight bars visible on a 15-minute chart. Without this, TradingView shows only Xetra hours and the Globex session disappears.

To set it: right-click the chart → **Settings** → **Symbol** tab → set **Session** to **Regular Trading Hours (RTH)**.

### Timezone

Set the chart timezone to **Europe/Berlin**. This ensures the session boundaries in the indicator (17:30, 08:00, 09:00) align correctly with the bar timestamps in the CSV.

To set it: click the time displayed at the **bottom right of the chart** → select **Europe/Berlin** from the list.

---

## Apply the indicator

If you haven't installed the indicator yet, do step 2 first, then come back here.

Once installed, open the **Data Window** panel (right side of TradingView, or press **Alt+D** / **Cmd+D**). Hover over a bar inside the Xetra session. You should see these values populating:

- Globex Range
- GX vs 8D Xetra
- Frankfurt vs 8D Xetra
- 8D Xetra Avg Range
- Is Bar 1 / Is Bar 2

If those are blank or showing `n/a`, check the timezone setting and confirm you are on a 15-minute chart with `FDAX1!`.

---

## Export the CSV

Click the **Export chart data** button — it is the small down-arrow icon at the top of the chart, or right-click the chart background and select **Export chart data**.

Settings to use in the export dialog:

- **Time format:** ISO (timestamps come out as `2024-01-15T09:00:00` rather than fractional numbers)
- Export all available columns

Click **Export**. A CSV downloads containing time, OHLCV, and all the Data Window values from the indicator.

Open it briefly to check:

- You should see columns including `time`, `open`, `high`, `low`, `close`, and the indicator outputs (`Globex Range`, `GX vs 8D Xetra`, `Frankfurt vs 8D Xetra`, etc.)
- The first 8 rows will have blank ABR values — the 8-bar average needs 8 bars to initialise. This is expected
- You should have bars spanning the full 24 hours of each trading day

---

## A note on data history limits

TradingView's history limit on 15-minute bars depends on your plan. Free accounts typically get around 1–2 years. A paid plan gives significantly more. The FDAX dataset included in `data/` was built by stitching multiple exports together — if your export is shorter, the study still works but covers a narrower date range.

---

Once you have the CSV, go to [step 3 — run the study](./03-run-the-study.md).
