# Step 3 — Run the Study

Paste the prompt below into your AI (Claude works best; ChatGPT also works) along with the CSV you exported in step 1. Attach the reference HTML from `reference-output/FDAX_Daily_Range_Distribution_v1_3_20260512.html` so the AI can see exactly what to mimic.

The AI will produce an HTML report and a markdown summary for your instrument, structured identically to the FDAX reference.

---

## What to attach

1. Your CSV export from TradingView (step 1)
2. The reference HTML report: `reference-output/FDAX_Daily_Range_Distribution_v1_3_20260512.html`
3. Optionally, the reference markdown: `reference-output/FDAX_Daily_Range_Distribution_Stats_v1_0_20260512.md`

---

## The prompt to paste

Copy everything between the `---PROMPT START---` and `---PROMPT END---` lines. The AI does the rest.

---PROMPT START---

I want you to run a Daily Range Distribution study on the attached CSV and produce two deliverables: an HTML report and a markdown stats summary. Mimic the style and structure of the attached FDAX reference report exactly.

## The data

The CSV is a daily-bar export from TradingView with these relevant columns:

- `time` — date of the bar
- `Range` — daily range in points (high − low)
- `Average Bar Range` — 8-bar simple moving average of Range
- `Range / ABR` — the ratio Range divided by Average Bar Range

The first ~7 rows will have a blank Average Bar Range (the moving average needs 8 bars to warm up). Drop these rows before analysis. Print the count of dropped rows.

If `Range / ABR` is missing or blank, compute it yourself as `Range ÷ Average Bar Range`. Treat that as the single value the analysis works on. I will refer to it as **Range X** from here on, matching the FDAX reference.

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

Mimic the attached FDAX HTML reference exactly. Same structure, same colours, same component patterns, same chart style. Substitute the instrument name and all the numbers.

The structure to follow:

1. **Header** with tag "◆ Quantitative Research", H1 "[INSTRUMENT] Daily Range Distribution", one-sentence subtitle, meta row with instrument / Daily / date range / N / version / date.

2. **Summary** section with six KPI cards in this order: Median (accent blue), Mean (slate), Std Dev (amber), Most Common Day (green), Min (purple), Max (red). Each card has a label, big value, and small sub-line. Below the KPIs, a blue note-box describing the distribution shape in one paragraph (right-skewed? where the body sits? where the tail starts?). Below that, an amber note-box titled "What the stats words mean" with plain-English bullet points for median, mean, std dev, and mode — copy the exact wording from the FDAX reference if you like, just swap the numbers.

3. **Data Universe** section with four KPI cards: Instrument, Timeframe (Daily), Days (N), Date Range.

4. **Range Distribution** section — the histogram chart. Spec is below.

5. **Range by Size Category** — single table with the six size buckets and a colour-coded pill for each percentage (slate / blue / green / amber / red / purple).

6. **Full Distribution Table** — every populated 0.1x bin with Band, Count, % of Days, Cumulative %. The "% of Days" column should be heat-mapped in green tint — darker green for higher percentages.

7. **Version History** — single row at v1.0 with today's date and "Initial release" in the changes column.

8. **Footer** with study name on the left, version on the right.

## The chart

A hand-drawn HTML canvas histogram, not a chart library. Critical points:

- Canvas height around 440px
- Bars at 0.1x ABR resolution
- Bar colours: slate (#64748B) for bins below 0.6x, purple (#7C3AED) for 0.6 to 2.0x, red (#DC2626) for 2.0x and above
- Value label above each bar where the percentage is at least 1%
- Left Y axis: % of days, with grid lines
- Right Y axis: cumulative %, 0–100% scale
- A blue cumulative-percentage line drawn on top of the bars
- X-axis tick labels every 0.2x
- Dashed vertical reference lines at median (green) and mean (amber), with labels above the plot area
- **The reference labels must be collision-aware** — median and mean are usually close together and their labels will overlap if drawn at the same y-coordinate. Track each label's x-position and offset the second one down by 14px if it's within 70px of the first.
- **The legend goes BELOW the canvas as HTML, not drawn on the canvas.** Six items: Quiet (slate), Body (purple), Tail (red), Cumulative % (blue line), Median (green line), Mean (amber line). This prevents the legend from being clipped on smaller screens.

## Style cheat-sheet (in case you need it)

Colours (CSS variables):

```css
--bg:#FAFAF8; --surface:#FFFFFF; --surface-alt:#F5F4F0;
--border:#E8E6E1;
--text-primary:#1A1A18; --text-secondary:#6B6964; --text-muted:#9C9890;
--accent:#2563EB; --green:#16A34A; --red:#DC2626;
--amber:#D97706; --purple:#7C3AED; --slate:#64748B;
```

Each colour also has a `-bg` (pale tint) and `-light` (even paler) variant for backgrounds. See the FDAX reference for exact values.

Fonts: DM Sans for prose and headings, JetBrains Mono for all numbers and labels. Loaded from Google Fonts.

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

UTF-8 only: include `<meta charset="UTF-8">`. No HTML entities, no BOM.

Single self-contained HTML file: inline `<style>` and inline `<script>`. No external CSS or JS files.

## The markdown summary

Also produce a plain markdown file with the data tables and key observations. Same structure as the attached FDAX markdown reference. Sections:

1. Title with instrument, version, date
2. Data Universe table
3. Summary Statistics table
4. Size Bucket Distribution table
5. Full Distribution table
6. Key Observations — **written from the actual numbers**, not copied from FDAX. Where does this instrument's mode sit? Where does the sharp drop happen? How fat is the tail?
7. Version History

## Filenames

- HTML: `[INSTRUMENT]_Daily_Range_Distribution_v1_0_[YYYYMMDD].html`
- Markdown: `[INSTRUMENT]_Daily_Range_Distribution_Stats_v1_0_[YYYYMMDD].md`

Replace `[INSTRUMENT]` with `ES`, `NK`, `HSI`, or whatever short code matches your instrument. `[YYYYMMDD]` is today's date.

## Things to get right

1. **Don't copy FDAX's Key Observations.** Write fresh ones from this instrument's actual numbers. The mode might not be 0.7-0.8x. The sharp drop might be at a different threshold. The tail might be heavier or lighter.

2. **Don't draw the chart legend on the canvas.** Always HTML below the canvas.

3. **Don't let the median and mean labels overlap.** Use the collision-aware approach described above.

4. **Don't silently drop ABR-null rows.** Print the dropped count first, then drop.

5. **Bins with very few days are noise.** Still show them in the table (don't filter), but the Key Observations should not be built off any bin with fewer than 10 days.

Confirm you understand the brief, show me the summary stats and histogram as text first, and then build the files.

---PROMPT END---

---

## After the AI is done

You'll have two files:

- An HTML report — open it in your browser to view
- A markdown summary — open in any text editor or markdown viewer

Compare the headline numbers to the reference FDAX report:

- **FDAX mean is 1.00x, median 0.95x.** A "normal" instrument should land somewhere similar. If your mean is wildly different (say 1.3x), check whether the AI dropped the ABR-null rows correctly.
- **FDAX has 1.87% of days above 2x ABR.** A heavier-tailed instrument might show 3-4%; a tamer one closer to 1%.
- **FDAX's mode is 0.7-0.8x.** Most equity indices land in the 0.7-0.9x range. Commodities sometimes show different mode positions.

If the numbers look implausible, ask the AI to re-print the summary stats and the row count, and to confirm it dropped the warm-up nulls.

---

## Cross-instrument comparison

Once you have reports for two or more instruments, you can compare them directly. The Range X normalisation means a 1.5x day on one instrument represents the same relative volatility as a 1.5x day on another. The size buckets and percentile cuts use the same definitions across all instruments.
