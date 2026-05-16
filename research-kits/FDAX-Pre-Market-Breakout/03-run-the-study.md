# Step 3 — Run the Study

This step walks you through replicating or extending the FDAX pre-market breakout analysis. Two paths are available: use the AI execution prompt with your own CSV, or browse the pre-built reference output directly.

---

## Option A — Browse the pre-built output

If you just want to see the results without running anything yourself, open `reference-output/index.html` in any browser. It is a self-contained interactive HTML report with all charts, KPI cards, and breakout distribution tables from the full 1,878-day study (Dec 2018 – May 2026).

The markdown summary `reference-output/FDAX_Pre_Market_Breakout_Stats_v2_0_20260516.md` contains every number in plain text, useful for copying into your own notes or running a cross-study comparison.

---

## Option B — Run it yourself with the execution prompt

Paste the prompt below into Claude (claude.ai) along with your CSV file. The prompt is self-contained and pre-written for FDAX. If you are adapting it to another instrument, read the adaptation notes at the bottom of this page first.

---

### Execution prompt

Paste this prompt verbatim, then attach your CSV file from step 1.

```
You are a quantitative trading researcher. Analyse the attached 15-minute FDAX futures CSV (from TradingView, Berlin time, continuous contract FDAX1!) and produce a pre-market breakout study.

## Instrument and sessions

- Instrument: FDAX (DAX Futures, Eurex), continuous contract
- Globex (overnight) session: 17:30 to 09:00 Berlin time (wraps midnight — prior day close through to RTH open)
- Frankfurt pre-open session: 08:00 to 09:00 Berlin time (the final hour before RTH)
- RTH (Xetra) session: 09:00 to 17:30 Berlin time

## Data

The CSV contains 15-minute bars. Each bar has a `time` column (ISO timestamp, Berlin timezone), plus OHLC. It also contains pre-computed indicator columns including:

- `Globex Range` — the high-to-low range of the Globex overnight session in points
- `GX vs 8D Xetra` — the Globex range as a fraction of the 8-bar rolling average daily Xetra range (ABR). This is the normalisation column used for bucketing.
- `Frankfurt vs 8D Xetra` — the Frankfurt pre-open range as a fraction of ABR
- `8D Xetra Avg Range` — the ABR value itself (8-day rolling average of daily Xetra high-to-low)
- `Is Bar 1` — flag (0 or 1) marking the first 15-minute bar of the Xetra RTH session (09:00 Berlin)

Use `Is Bar 1 == 1` to identify the RTH open for each trading day. Do not recompute the session ranges — use the pre-computed columns directly.

## Analysis steps

### Step 1 — Build the daily row

For each trading day (each row where `Is Bar 1 == 1`):
- Identify the Globex Range and GX vs 8D Xetra values at the Bar 1 timestamp
- Identify the Frankfurt Range and Frankfurt vs 8D Xetra values at the Bar 1 timestamp
- Identify the ABR (8D Xetra Avg Range) at Bar 1
- Compute the RTH high and RTH low across all 15-minute bars from 09:00 to 17:30 (inclusive of both boundary bars)
- Reconstruct the Globex high and Globex low directly: scan backward from Bar 1 to find the prior session's Bar 1 (the previous day's 09:00), then take the max high and min low of all bars from that prior Bar 1 onward through 09:00 today. That gives you the Globex high and low.
- The Frankfurt high = max high of all bars from 08:00 to the bar immediately before 09:00 (exclusive). The Frankfurt low = min low of those same bars.

### Step 2 — Classify each day

Globex breakout:
- Broke High Only: RTH high > Globex high AND RTH low >= Globex low
- Broke Low Only: RTH low < Globex low AND RTH high <= Globex high
- Broke Both: RTH high > Globex high AND RTH low < Globex low
- Neither: RTH high <= Globex high AND RTH low >= Globex low

Frankfurt breakout (same logic, applied to Frankfurt high/low):
- Broke High Only, Broke Low Only, Broke Both, Neither

Classification is path-independent — you only need the session-high and session-low, not the intrabar sequence. There are no unresolvable cases.

### Step 3 — Bucket by range size

Bucket the GX vs 8D Xetra ratio into the following groups:
0-30%, 30-40%, 40-50%, 50-60%, 60-70%, 70-80%, 80-90%, 90-100%, 100-120%, 120%+

Bucket the Frankfurt vs 8D Xetra ratio into:
0-10%, 10-15%, 15-20%, 20-25%, 25-30%, 30-35%, 35-40%, 40-50%, 50%+

For each bucket, count and percentage-breakdown by breakout type.

### Step 4 — Summary statistics

Compute:
- Overall breakout rates for Globex (% High Only, % Low Only, % Both, % Neither)
- Overall breakout rates for Frankfurt
- "At least one side broken" rate for both ranges
- "Both" rate and "Neither" rate as the headline structural stats
- For the structural trend: confirm whether "Both" collapses and "Neither" rises monotonically as GX/ABR increases

## Output

Produce a single self-contained HTML file with:
- A header section with instrument name, date range, and total day count
- KPI cards for the headline numbers (Globex breakout rate, Frankfurt breakout rate, Both rate, Neither rate)
- A Globex breakout distribution chart (canvas bar chart, bucketed by GX/ABR)
- A Frankfurt breakout distribution chart (canvas bar chart, bucketed by FF/ABR)
- A data table for each bucketed breakdown
- A findings section summarising the structural pattern in plain language

Use a professional dark-background institutional style (dark navy/charcoal background, DM Sans body font, JetBrains Mono for numbers, coloured accent lines for chart series).

State upfront whether you are using pre-computed columns or recomputing from scratch. State the total number of trading days found (Is Bar 1 == 1 count) and the date range before proceeding.
```

---

### What to expect

The prompt takes 2–5 minutes to run on a full 7-year dataset depending on the length of the CSV and your account's context limit. It will first confirm the day count and date range, then work through the classification and bucketing, then produce the HTML.

If the output is cut short due to context length, paste the prompt again and add: "The previous run was cut short at [point]. Continue from that point using the same data."

---

### Reviewing the output

Once the HTML is produced, save it locally and open it in a browser. Check:

1. **Day count** matches your expectation from the CSV date range
2. **Frankfurt breakout rate** should be close to 100% — if it's materially lower (below 95%), the Frankfurt session extraction likely has a timezone or boundary issue
3. **Structural pattern** — "Both" should fall and "Neither" should rise as GX/ABR increases. If this pattern is absent, the Globex high/low reconstruction may be using the wrong bars

---

## Adapting to another instrument

The prompt above is written for FDAX with Berlin-time session boundaries. To adapt it:

1. Change the session times to match your instrument (e.g. for ES: Globex = 17:00–09:30 ET, pre-market = 08:00–09:30 ET, RTH = 09:30–16:00 ET)
2. Change the timezone in the CSV instructions to match your TradingView export timezone
3. Change the normalisation baseline — for ES the ABR column is based on the NYSE session range, not Xetra
4. Adjust the Frankfurt bucket breakpoints if the pre-open window is a different fraction of the day's range for your instrument

---

[Back to README](./README.md)
