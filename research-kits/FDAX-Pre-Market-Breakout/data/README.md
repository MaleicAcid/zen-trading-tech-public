# Data

This folder contains a pre-built stitched 15-minute FDAX dataset used in the pre-market breakout study.

| File | Description |
|------|-------------|
| `FDAX_15min_stitched_20181221_to_20260515.csv` | 153,123 bars, Dec 2018 – May 2026. Built by stitching multiple TradingView exports and deduplicating on timestamp. Timestamps are in Europe/Berlin timezone (ISO format). |

To use this file with the study, follow the instructions in [03-run-the-study.md](../03-run-the-study.md).

To build your own dataset instead, follow [01-download-data.md](../01-download-data.md).
