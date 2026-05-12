# Zen Average Bar Range Stats — Daily Range Profiling Helper

A minimal **TradingView Pine Script v5 indicator** that computes the three values needed for a daily range distribution study and exposes them in the Data Window only. Nothing is rendered on the chart. Designed to be applied on a daily-timeframe chart and then exported via TradingView's "Export chart data" feature.

---

## What it does

Adds three columns to the CSV export from TradingView, alongside the standard OHLC:

| Column | Definition |
|---|---|
| **Range** | `high − low` for the bar, in points |
| **Average Bar Range** | N-bar simple moving average of Range (default N = 8) |
| **Range / ABR** | Range divided by Average Bar Range — the normalised ratio |

The indicator does not draw anything on the chart and does not add a separate pane. The values exist only in the Data Window panel, where TradingView's export mechanism picks them up automatically.

---

## Why it exists

If you want to study how daily range behaves on an instrument — how often a quiet day occurs, where the fat tail starts, what counts as "typical" — you need a way to normalise range across instruments and across time periods. Raw points don't compare: 500 points on the S&P E-mini and 500 points on the Nikkei mean very different things, and 500 points in 2010 means something different from 500 points in 2025.

The standard normalisation is to express each day's range as a multiple of recent average range. That's the **Range / ABR** ratio this indicator computes. With it, a "1.5x day" on any instrument in any era means the same thing: today was 1.5 times the recent 8-day average.

This indicator is the minimum tool needed to produce that ratio. Three lines of output, no chart clutter, ready for CSV export.

---

## How to install

This is a **Pine Script v5** indicator for TradingView.

1. Open the `Average_Bar_Range_Stats_v1_1_20260512.txt` file in this folder and **copy the entire contents**
2. In TradingView, open the **Pine Editor** (bottom panel)
3. **Paste** the code into a new script
4. Click **Save** (give it a name) then **Add to chart**
5. Open the **Data Window** panel on the right of the chart — the three new columns appear there

> The source is provided as a `.txt` file rather than `.pine` so it renders cleanly on GitHub and copy-pastes straight into the Pine Editor without a download step.

---

## How to use the exported data

1. Apply the indicator on the **daily** timeframe of any instrument
2. Right-click the chart → **Export chart data**
3. Choose CSV — you'll get OHLC plus Range, Average Bar Range, and Range / ABR
4. The first 7 rows will have blank Average Bar Range values from the moving-average warm-up period — drop these rows before analysis

---

## Inputs

| Input | Default | Notes |
|---|---|---|
| Average Bar Range Length | 8 | Number of bars in the simple moving average. 8 is the convention used across the Zen Trading Tech research library. |

---

## Notes on the calculation

- **Range = `high − low`**, intraday range only. Gaps are **not** included. This is intentional — for cross-instrument comparability in a distribution study, every instrument needs the same definition. Some indicators use *true range* (which includes gaps); this one does not.
- The Average Bar Range is a **simple** moving average. Other averages (EMA, RMA, etc.) produce different smoothing characteristics and are not directly comparable.

---

## License

MIT. Free to use, modify, and share. Attribution to [Zen Trading Tech](https://zentradingtech.com) appreciated.
