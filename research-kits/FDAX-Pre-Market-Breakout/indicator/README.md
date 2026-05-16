# Zen-DAX GX v11 — Indicator Guide

A TradingView Pine Script v5 indicator that draws the Globex overnight range and Frankfurt pre-open range on an FDAX 15-minute chart, exposes session metrics in the Data Window for CSV export, and shows a regime label classifying the overnight range relative to the 8-day Xetra average range (ABR).

This is the indicator used to produce the pre-market breakout research in this kit.

---

## What it draws on the chart

| Visual | Description |
|--------|-------------|
| Globex box (orange) | High and low of the overnight session (17:30–09:00 Berlin) |
| Globex extension lines | Horizontal levels extending into the Xetra session |
| Globex fractional lines | 33%, 50%, 66% of the overnight range |
| Frankfurt box (blue) | High and low of the pre-open hour (08:00–09:00 Berlin) |
| Frankfurt extension lines | Horizontal levels extending into the Xetra session |
| Frankfurt fractional lines | 33%, 50%, 66% of the Frankfurt range |
| Regime label | Classifies the overnight range as TIGHT / MEDIUM / WIDE with breakout probabilities |

Everything is toggleable via the indicator settings panel.

---

## What it exposes in the Data Window

These values are visible when you hover over any bar with the Data Window panel open. They are the values that get exported to CSV for the research study.

| Data Window label | Description |
|-------------------|-------------|
| Globex Range | Overnight range in points |
| GX%D | Globex range as % of the Xetra open price |
| GX vs 8D Xetra | Globex range / 8-day average Xetra range (ABR) |
| Frankfurt vs 8D Xetra | Frankfurt range / 8-day average Xetra range (ABR) |
| 8D Xetra Avg Range | The ABR normaliser value |
| Daily Xetra Range | Full Xetra session range for the day |
| Is Bar 1 / Is Bar 2 | Flags the first and second 15-min bars of the Xetra session |
| Bar 2 Close/High/Low vs Frankfurt | Relationship of Bar 2 to the Frankfurt range |
| Bar 2 Close/High/Low vs Globex | Relationship of Bar 2 to the Globex range |

---

## Regime label

At the open of each Xetra session (Bar 1), the indicator calculates GX%D and displays a label:

| Regime | GX%D | What it means |
|--------|------|---------------|
| TIGHT | < 0.5% | Overnight range is small relative to the Xetra open price |
| MEDIUM | 0.5% – 1.0% | Typical overnight range |
| WIDE | > 1.0% | Large overnight move — market has already covered significant ground |

The label also shows the historical breakout probabilities from the research (Both sides broken, Neither side broken) so you can see the context at a glance each morning.

---

## Session times

All sessions use **Europe/Berlin** timezone by default. This is configurable in the indicator settings.

| Session | Default time (Berlin) |
|---------|-----------------------|
| Globex / Overnight | 17:30 – 09:00 (wraps midnight) |
| Frankfurt pre-open | 08:00 – 09:00 |
| Xetra | 09:00 – 17:30 |

---

## Bar 2 features

Bar 2 is the second 15-minute bar of the Xetra session (09:15–09:30 Berlin). The indicator optionally highlights Bar 2 and draws extension lines from its high and low. These levels are used as the breakout trigger in the trade management logic.

The trade management logic (Bar 2 breakout entry, stop, target) is included in the indicator but disabled by default. Enable via **Trade Management** settings.

---

## Installation

1. Copy the full contents of `Zen_DAX_GX_v11.txt`
2. In TradingView, open the **Pine Editor** (bottom of the screen)
3. Clear the default template and paste the code
4. Click **Save**, then **Add to chart**
5. Set the chart to **15-minute** timeframe on `FDAX1!` (continuous contract)
6. Set the chart timezone to **Europe/Berlin**
7. Open the **Data Window** panel and verify the values are populating

See `../02-install-indicator.md` for full step-by-step instructions.
