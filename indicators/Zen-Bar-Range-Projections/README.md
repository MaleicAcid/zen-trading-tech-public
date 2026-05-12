# Zen Bar Range Projections — Dual HTF ABR Levels

A TradingView Pine Script indicator that projects **0.5×, 1×, and 2× ABR levels above and below the close of two independent higher timeframes**. Useful for seeing where measured moves from the most recent closed HTF bar land relative to current price, without drawing the lines manually.

---

## What it does

For each of two configurable higher timeframes, the indicator takes the close of the most recently completed HTF bar and the ABR (Average Bar Range) over that timeframe, and draws short horizontal reference lines:

- **±1× ABR** (solid)
- **±0.5× ABR** (dashed)
- **±2× ABR** (dotted, off by default)

Each projection set is anchored at the last chart bar of the closed HTF bar and extends a configurable number of bars to the right. The HTF close and HTF ABR are sourced from the last completed HTF bar — not the forming one — so the lines do not drift while the live HTF bar is in progress.

A **Bars Back** input fans out up to twelve historical projection sets per timeframe so you can audit how price has interacted with prior levels (useful for visual backtesting and gauging whether 1× or 2× is a meaningful magnet on the instrument and timeframe you trade).

The two HTF projections are fully independent: each has its own timeframe, lookback, bars back, line length, line thickness, level toggles, and colours. The second HTF defaults to a thicker line and contrasting colour scheme so the two levels remain visually distinct when stacked on the same chart.

---

## How to install

This is a **Pine Script v6** indicator for TradingView. To use it:

1. Open the `Zen_Bar_Range_Projections_v2.1_20260509.txt` file in this folder and **copy the entire contents**
2. In TradingView, open the **Pine Editor** (bottom panel)
3. **Paste** the code into a new script
4. Click **Save** (give it a name) then **Add to chart**
5. Configure inputs via the gear icon on the indicator

> The source is provided as a `.txt` file rather than `.pine` so it renders cleanly on GitHub and copy-pastes straight into the Pine Editor without a download step.

---

## Inputs

Each HTF group has the same input set. Defaults shown for HTF 1 / HTF 2.

### HTF 1 / HTF 2

| Input | HTF 1 default | HTF 2 default | Notes |
|---|---|---|---|
| Enable | On | On | Master toggle for the HTF group. |
| Timeframe | 15 | 60 | Standard TradingView timeframe strings (`15`, `60`, `240`, `D`, `W`). |
| ABR Lookback | 8 | 8 | Number of completed HTF bars used to compute Average Bar Range. |
| Bars Back | 10 | 5 | `0` = one projection set anchored at the last completed bar. `11` = twelve sets fanned back through history. |
| Line Length (bars) | 2 | 4 | How far to the right of the anchor each line extends, in chart bars. |
| Line Thickness | 1 | 2 | Stroke thickness, 1–4. Higher TF defaults to thicker. |
| Show 0.5× | On | On | Toggle the half-ABR projection levels. |
| Show 1× | On | On | Toggle the full-ABR projection levels. |
| Show 2× | Off | Off | Toggle the double-ABR projection levels. |

### Colours

Each HTF group has six configurable colours: 0.5× up, 0.5× down, 1× up, 1× down, 2× up, 2× down.

| HTF | Up default | Down default |
|---|---|---|
| HTF 1 | Blue | Red |
| HTF 2 | Green | Orange |

---

## How to read it

The **1× ABR** levels mark a full average bar range above and below the prior HTF close. Reaching +1× or −1× means price has travelled the average bar's distance away from the prior HTF close — a reference for whether the current move is stretched or still in normal range.

The **0.5× ABR** levels are the halfway markers. They tend to be touched more frequently and act as midpoint references inside an active HTF bar.

The **2× ABR** levels mark a double-range extension. Reaching these levels is statistically less common and indicates a high-momentum or trending bar relative to recent HTF volatility. Disabled by default to keep the chart clean — enable on a per-HTF basis when you want extension targets.

In dual-HTF mode (both HTFs enabled simultaneously) the typical setup is a faster TF for short-term reference (e.g. 15m on a 5m chart) and a slower TF for context (e.g. 60m or daily). The thicker, contrasting HTF 2 colours make it easy to read both layers without confusion.

Use the **Bars Back** input to fan out historical projections and visually check how often price stops at, hesitates at, or blows through each level on the instrument and timeframe you trade. This is the cheapest way to gauge whether a level matters before relying on it live.

---

## Version

**v2.1** — current.

- Dual independent HTF projections in a single indicator (replaces the prior workflow of stacking two copies of the indicator)
- Added 2× ABR projection level (toggleable, off by default)
- Configurable line thickness per HTF
- Bars Back independent per HTF
- Renamed "Line Width" to "Line Length" for clarity
- HTF data sourcing pattern: `[close[1], (high - low)[1]]` inside `request.security()` with `lookahead_on`. This returns the closed HTF bar's close and range directly on every chart bar, eliminating the cross-timeframe drift previously seen on cold chart loads.

---

## License

MIT. Free to use, modify, and share.
