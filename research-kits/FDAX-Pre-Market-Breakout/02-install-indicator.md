# Step 2 — Install the Indicator

This step adds the Zen-DAX GX v11 indicator to your TradingView chart. It draws the Globex and Frankfurt session boxes, extension lines, and fractional levels, and exposes session metrics in the Data Window for CSV export.

---

## Install

1. Open `indicator/Zen_DAX_GX_v11.txt` from this kit and copy the entire contents.
2. In TradingView, open the **Pine Editor** — it's the tab at the bottom of the screen. If you don't see it, look for the toggle in the bottom toolbar.
3. Clear the default template (select all, delete) and paste the copied code.
4. Click **Save** at the top of the Pine Editor. Name it — for example, "Zen-DAX GX v11".
5. Click **Add to chart**.

---

## Chart setup

Before confirming the indicator is working, make sure your chart is set up correctly:

- **Symbol:** `FDAX1!` (continuous futures contract)
- **Timeframe:** 15 minutes
- **Session:** RTH — right-click the chart → Settings → Symbol tab → Session → Regular Trading Hours
- **Timezone:** Europe/Berlin — click the time at the bottom right of the chart and select Europe/Berlin

These settings matter. The indicator's session boundaries (17:30, 08:00, 09:00) are defined in Berlin time. If the timezone is wrong, the boxes will appear at the wrong times.

---

## Confirm it's working

Open the **Data Window** panel on the right side of TradingView. Keyboard shortcut: **Alt+D** (Windows) or **Cmd+D** (Mac).

Navigate to a bar inside the Xetra session (between 09:00 and 17:30 Berlin time). The Data Window should show:

```
Zen-DAX GX v11
  Is Bar 1                  0 or 1
  Is Bar 2                  0 or 1
  Bar 1 Bull/Bear           -1, 0, or 1
  Bar 2 Bull/Bear           -1, 0, or 1
  Globex Range              e.g. 142.5
  GX%D                      e.g. 0.75  (Globex range as % of that day's Xetra range)
  GX vs 8D Xetra            e.g. 0.58
  Frankfurt vs 8D Xetra     e.g. 0.21
  8D Xetra Avg Range        e.g. 248.0
  Daily Xetra Range         e.g. 198.0
```

If those values are populating, the indicator is working correctly.

If values are showing as `n/a` or blank:
- Check you are on a **15-minute** chart — the session logic does not work on daily bars
- Check the **timezone is set to Europe/Berlin**
- Check the **session is set to RTH** so overnight bars are visible
- Make sure you are hovering over a bar **during the Xetra session**, not overnight — some values only populate during 09:00–17:30

---

## What you'll see on the chart

Once applied to a correctly configured chart you will see:

- An **orange box** spanning the Globex overnight session high and low, with extension lines running into the Xetra session
- A **blue box** spanning the Frankfurt pre-open hour (08:00–09:00), with extension lines
- **Dotted purple lines** at 33%, 50%, and 66% of both the Globex and Frankfurt ranges
- A **regime label** at the Xetra open classifying the overnight range as TIGHT / MEDIUM / WIDE with historical breakout probabilities

All visuals are toggleable in the indicator settings panel (double-click the indicator name in the chart legend).

---

## Indicator settings overview

| Group | Key settings |
|-------|-------------|
| Time Settings | Timezone (default: Europe/Berlin), session times |
| Globex Visuals | Toggle box, extension lines, label; colours |
| Frankfurt Visuals | Toggle box, extension lines, label, fractional lines; colours |
| Globex Fractional Lines | Toggle 33/50/66% lines; colour and style |
| Globex Regime Analysis | Toggle regime label; size and position |
| RTH Bar 2 Visuals | Highlight Bar 2, extension lines from Bar 2 high/low |
| Risk/Reward Targets | Draw 1R and 2R target lines from Bar 2 |
| Trade Management | Bar 2 breakout entry logic with stop and target tracking |
| Stats Display | On-chart win/loss table for the Bar 2 trade logic |

For the purposes of data export and replication of the research study, the default settings are fine — no changes needed.

---

Once installed and confirmed working, go to [step 3 — run the study](./03-run-the-study.md).
