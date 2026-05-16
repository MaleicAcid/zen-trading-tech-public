# FDAX Pre-Market Breakout — Research Kit

A self-contained kit covering the statistical behaviour of the FDAX overnight (Globex) and Frankfurt pre-open ranges relative to Xetra price action — how often Xetra breaks each range, which direction, and how breakout shape changes as the overnight range grows.

The study was run on 1,878 trading days (Dec 2018 – May 2026) using a stitched 15-minute FDAX history built from the Zen-DAX GX indicator. The same methodology can be applied to any futures instrument with a defined pre-market session.

---

## What the research shows

- **Xetra breaks the Globex range 94.1% of days** — one or both sides
- **Xetra breaks the Frankfurt range 99.9% of days** — exactly one "Neither" day in 7.4 years, during peak COVID volatility
- **Frankfurt "Both" sides broken: 62.4%** — rises to 87% when the Frankfurt range is under 10% of ABR
- **Overnight range size predicts breakout shape, not daily size** — as the Globex range grows from <30% to 120%+ of ABR, "Both" collapses from 42% to 3% and "Neither" rises from 0% to 31%
- **Correlation between Globex range and daily range: r = 0.28** — weak; a big overnight range tells you how Xetra will behave relative to it, not how large the Xetra session will be

---

## What's in this kit

| Item | Location |
|------|----------|
| Full HTML report | `reference-output/index.html` |
| Markdown stats summary | `reference-output/FDAX_Pre_Market_Breakout_Stats_v2_0_20260516.md` |
| 15-minute FDAX data (stitched) | `data/` |
| Zen-DAX GX indicator (Pine v5) | `indicator/Zen_DAX_GX_v11.txt` |
| Indicator guide | `indicator/README.md` |
| Data download guide | `01-download-data.md` |
| Indicator install guide | `02-install-indicator.md` |
| Replication prompt | `03-run-the-study.md` |

---

## How to use this kit

**To read the research:** open the HTML report in any browser. The markdown summary contains every number in plain text for easy reference or cross-study comparison.

**To replicate or extend the study:** work through the three numbered guides in order. You can run the same study on any futures instrument with a defined pre-market session — ES, NQ, HSI, Nikkei, or others. The execution prompt in step 3 is pre-written; drop in your CSV and run it.

**To visualise the levels on a live chart:** install the Zen-DAX GX indicator from the `indicator/` folder. It draws the Globex and Frankfurt boxes, extension lines, fractional levels, and regime labels directly on your TradingView chart.

---

## Session definitions

| Session | Time (Berlin / Europe/Berlin) |
|---------|-------------------------------|
| Globex / Overnight | 17:30 previous day – 09:00 |
| Frankfurt pre-open | 08:00 – 09:00 |
| Xetra | 09:00 – 17:30 |

ABR = 8-day rolling average of the daily Xetra range, used as the normaliser throughout.

---

## License

MIT. Free to use, modify, share. Attribution to [Zen Trading Tech](https://zentradingtech.com) appreciated.
