# Zen Bar Range Projections

A TradingView Pine Script indicator that projects **0.5x and 1x ABR levels above and below the close of the prior bar** - either on the chart timeframe or on a higher timeframe of your choice. Useful for seeing where a measured move from the last completed bar lands relative to current price, without drawing the lines manually.

---

## What it does

For each projection set, the indicator takes the close of the prior completed bar and the ABR (Average Bar Range) over a configurable lookback, and draws four short reference lines:

- **+1x ABR** above the close (solid, blue by default)
- **+0.5x ABR** above the close (dashed)
- **-0.5x ABR** below the close (dashed)
- **-1x ABR** below the close (solid, red by default)

The projection set is anchored at the close of the prior bar and extends a few bars to the right so it doesn't clutter the live bar.

There are two modes:

- **Chart TF** - uses the chart's own prior bar close and chart-timeframe ABR. Use this when you want a measured move from the last completed bar at the timeframe you're looking at.
- **Higher TF** - uses the last closed bar from a higher timeframe (e.g. 60-minute, daily) and the HTF ABR. The HTF close and HTF ABR are pulled from the *last completed* HTF bar, not the forming one, so the lines don't drift while the HTF bar is in progress.

A **Bars Back** input fans out up to 12 historical projection sets so you can audit how price has interacted with prior projections (useful for visual backtesting and gauging whether 1x is a meaningful magnet on the instrument and timeframe you're looking at).

---

## How to install

This is a **Pine Script v6** indicator for TradingView. To use it:

1. Open `zen-bar-range-projections-v1.5.txt` in this folder and copy the entire contents.
2. In TradingView, open the **Pine Editor** (bottom panel).
3. Paste the code into a new script.
4. Click **Save** (give it a name) then **Add to chart**.
5. Configure inputs via the gear icon on the indicator.

---

## Inputs

### Settings
| Input | Default | Notes |
|---|---|---|
| Mode | Chart TF | `Chart TF` uses the chart's own bars. `Higher TF` uses the higher-timeframe bars set below. |
| Higher Timeframe | 60 | Only used when Mode is `Higher TF`. Standard TradingView timeframe strings (e.g. `60`, `240`, `D`, `W`). |
| ABR Lookback (bars) | 8 | Number of bars used to compute Average Bar Range. Applies to both Chart TF and Higher TF modes. |
| Bars Back | 0 | `0` = one projection set anchored at the last completed bar. Up to `11` = twelve sets fanned back through history. |
| Line Width (bars) | 2 | How far to the right of the anchor each projection line extends, measured in bars. |

### Colours
| Input | Default | Notes |
|---|---|---|
| 1x ABR up colour | Blue (solid) | Solid line at +1x ABR above the close. |
| 0.5x ABR up colour | Blue (50% transparency) | Dashed line at +0.5x ABR above the close. |
| 1x ABR down colour | Red (solid) | Solid line at -1x ABR below the close. |
| 0.5x ABR down colour | Red (50% transparency) | Dashed line at -0.5x ABR below the close. |

---

## How to read it

The 1x ABR levels mark a **full average bar range** above and below the prior close. On any given bar, reaching the +1x or -1x level means price has travelled the average bar's distance away from the prior close - a reference for whether the current bar is "stretched" or still in normal range.

The 0.5x levels are the halfway markers. They tend to be more frequently touched and act as midpoint reference inside an active bar.

In **Higher TF** mode the projections are stickier - a single set of lines sits on the chart for the duration of the HTF bar, giving an intraday trader a constant reference for "where is 1x of the last HTF bar's average range?"

Use the **Bars Back** input to fan out historical projections and visually check how often price stops at, hesitates at, or blows through the 1x level on the instrument and timeframe you're looking at. This is the cheapest way to gauge whether the level matters before relying on it live.

---

## Version

**v1.5** - current. Higher-timeframe mode now sources HTF close and HTF ABR from the last completed HTF bar (via `[1]` inside `request.security()`), so projection lines no longer drift while the live HTF bar is forming.

---

## License

MIT. Free to use, modify, and share.