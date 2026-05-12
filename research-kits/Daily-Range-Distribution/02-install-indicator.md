# Step 2 — Install the Indicator

This step adds a small Pine Script indicator to TradingView that computes three values per day and exposes them in the Data Window, ready to be picked up by the CSV export in step 1.

The indicator does not draw anything on the chart. Your chart stays exactly as it was — the values only live in the Data Window panel on the right.

---

## What it computes

Three columns:

| Column | Definition |
|---|---|
| **Range** | `high − low` for the bar, in points |
| **Average Bar Range** | 8-bar simple moving average of Range (length is configurable) |
| **Range / ABR** | Range divided by Average Bar Range — the normalised ratio |

The third one is the key value the study analyses. Expressing today's range as a multiple of the recent average makes the numbers comparable across instruments and across eras.

---

## Install

1. Copy the entire contents of `indicator/Average_Bar_Range_Stats_v1_1_20260512.txt` from this folder.
2. In TradingView, open the **Pine Editor** — it's at the bottom of the screen. If you don't see it, the toggle is in the menu bar at the bottom.
3. **Paste** the code into a new script (clear out the default `// This source code...` template first).
4. Click **Save** at the top of the Pine Editor. Give it a name like "Average Bar Range Stats" or whatever you like.
5. Click **Add to chart** (the button next to Save).

That's it. The indicator is now applied to your chart.

---

## Confirm it's working

Open the **Data Window** panel — it's the right-hand pane in TradingView, usually toggleable via a small icon on the right side. Keyboard shortcut: **Alt + D** (or Cmd + D on Mac).

Hover over any bar on the chart. The Data Window should show, among other things:

```
Average Bar Range Stats
  Range              ...
  Average Bar Range  ...
  Range / ABR        ...
```

If those three values appear, you're done.

If you don't see them, the indicator wasn't applied to this chart. Check the indicator legend at the top-left of the chart — "Average Bar Range Stats" should be listed. If it isn't, click **Add to chart** again from the Pine Editor.

---

## Inputs you can change

The indicator has one input:

- **Average Bar Range Length** — default 8. The number of bars in the simple moving average.

The Zen Trading Tech research convention is 8 bars. If you change this, your output won't be directly comparable to the reference FDAX numbers in this kit, but the methodology still works.

---

Once installed, go back to [step 1](./01-download-data.md) if you haven't exported the CSV yet, then on to [step 3](./03-run-the-study.md).
