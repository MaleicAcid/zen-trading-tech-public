# Daily Range Distribution — Research Kit

A self-contained kit for profiling how an instrument's daily range is distributed, expressed as a multiple of recent average range. Drop the CSV from TradingView into an AI chat with the execution prompt, and out comes an HTML report you can compare to the reference FDAX output included here.

The same kit works on any futures or cash instrument with sufficient daily history — ES, FDAX, NQ, RTY, YM, Nikkei, Hang Seng, gold, oil, individual stocks, anything. The output is normalised so different instruments can be compared apples-to-apples.

---

## What you end up with

An HTML report containing:

- The shape of the daily range distribution, as a histogram in 0.1x ABR bins
- A summary of the typical day, the average day, the spread, and the extremes
- A plain-English explainer of the stats terms
- A size-bucket breakdown (quiet / small / normal / large / big / outlier)
- A full distribution table with a green heat-map on the percentage column

See `reference-output/FDAX_Daily_Range_Distribution_v1_2_20260512.html` for an example built on 19 years of FDAX history.

---

## How to use this kit

The kit has four steps. Each step is its own document.

1. **[Download the data from TradingView](./01-download-data.md)** — apply the indicator, set the timeframe, export to CSV.
2. **[Install the indicator](./02-install-indicator.md)** — Pine v5 source ready to paste into TradingView's Pine Editor.
3. **[Run the study](./03-run-the-study.md)** — the prompt to paste into Claude (or any capable AI) along with your CSV.
4. **Reference output** — `reference-output/` folder containing the FDAX report. The AI is asked to mimic its style.

Work through them in order. The whole thing takes about 10 minutes once you have the indicator installed.

---

## What you'll need

- A TradingView account (free tier works for the data export)
- An AI chat that can read CSVs and write HTML — Claude is the recommended choice; ChatGPT works too
- Around 5 minutes of AI processing time once the prompt is pasted

---

## Why bother

If you trade an instrument and you don't know how its daily range is distributed, you're guessing about every stop, every target, and every "is today a big day or a quiet day" question. The distribution is the foundation. Everything else — measured moves, intraday targets, position sizing — rests on knowing what "normal" looks like for your instrument.

The same study run on four different instruments tells you whether their distributions are similar (often they're not), where each one's fat tail begins, and which days are genuinely rare.

---

## License

MIT. Free to use, modify, share. Attribution to [Zen Trading Tech](https://zentradingtech.com) appreciated.
