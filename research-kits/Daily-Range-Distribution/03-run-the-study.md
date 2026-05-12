# Step 3 — Run the Study

Paste the prompt below into your AI (Claude works best; ChatGPT also works) along with these attachments:

1. Your CSV export from TradingView (step 1)
2. The reference HTML report: `reference-output/FDAX_Daily_Range_Distribution_v1_3_20260512.html`
3. The reference markdown: `reference-output/FDAX_Daily_Range_Distribution_Stats_v1_0_20260512.md`

---PROMPT START---

I want you to run a Daily Range Distribution study on the attached CSV and produce two deliverables: an HTML report and a markdown stats summary. Mimic the style and structure of the attached FDAX reference report exactly.

## The data

The CSV is a daily-bar export from TradingView with these relevant columns:

- `time` — date of the bar
- `Range` — daily range in points (high − low)
- `Average Bar Range` — 8-bar simple moving average of Range
- `Range / ABR` — the ratio Range divided by Average Bar Range

Drop rows where `Average Bar Range` is null and print the count of dropped rows. Refer to `Range / ABR` as **Range X** throughout, matching the FDAX reference.

## What to compute

1. **Summary stats** on Range X across all clean rows:
   - Count of clean rows
   - Date range (first to last)
   - Mean, median, standard deviation
   - Min, max
   - Percentiles: P10, P25, P50, P75, P90, P95, P99

2. **Histogram of Range X at 0.1x bins** from 0.0 up to the max observed (round up to nearest 0.1). For each bin produce:
   - Lower edge, upper edge
   - Count of days in the bin
   - Percentage of clean days
   - Cumulative percentage

3. **Size buckets** — counts and percentages for:
   - Quiet: < 0.6x
   - Small: 0.6 – 0.8x
   - Normal: 0.8 – 1.2x
   - Large: 1.2 – 1.5x
   - Big: 1.5 – 2.0x
   - Outlier: ≥ 2.0x

4. **Mode** — the 0.1x bin with the highest count of days. Note both the band (e.g. "0.7-0.8x") and the % of days in it.

**Print all of the above as plain text tables in chat before generating the report files.** Wait for my confirmation if anything looks off.

## The HTML report

Mimic the attached FDAX HTML reference exactly — same structure, same components, same colours, same chart style. Substitute instrument name and numbers. Single self-contained HTML file.

Two things the reference won't make obvious:

- **Collision-aware median/mean labels.** Median and mean are usually close together and their labels will overlap if drawn at the same y-coordinate. Track each label's x-position and offset the second one down by 14px if it's within 70px of the first.
- **Legend goes BELOW the canvas as HTML, not drawn on the canvas.** Prevents clipping on smaller screens.

## The markdown summary

Mimic the attached FDAX markdown reference structure. Write fresh **Key Observations** from this instrument's actual numbers — don't copy FDAX's. Where does the mode sit? Where does the sharp drop happen? How fat is the tail?

## Filenames

- HTML: `[INSTRUMENT]_Daily_Range_Distribution_v1_0_[YYYYMMDD].html`
- Markdown: `[INSTRUMENT]_Daily_Range_Distribution_Stats_v1_0_[YYYYMMDD].md`

Replace `[INSTRUMENT]` with `ES`, `NK`, `HSI`, or whatever short code matches your instrument. `[YYYYMMDD]` is today's date.

## One more rule

Confirm you understand the brief, show me the summary stats and histogram as text first, and then build the files.

---PROMPT END---
