# FDAX Daily Range Distribution -- Stats v1.0 -- 20260512

How daily range as a multiple of 8-bar ABR is distributed across 19 years of FDAX history. This document is the data-only companion to the HTML report.

---

## Data Universe

| Item | Value |
|------|-------|
| Instrument | FDAX DAX Futures |
| Exchange | EUREX |
| Timeframe | Daily (1440 min) |
| Date range | 2007-03-13 -- 2026-05-11 |
| Total trading days | 4,856 |
| Study type | Profiling study |
| Source | TradingView export with Average Bar Range Stats indicator applied |

ABR = 8-bar SMA of daily range. Range X = today's range / ABR.

---

## Summary Statistics

| Metric | Value | Description |
|--------|-------|-------------|
| Median (P50) | 0.946x | typical day -- half of days are smaller, half are larger |
| Mean | 1.004x | arithmetic average |
| Standard Deviation | 0.379x | how much days vary around the mean |
| Mode | 0.7-0.8x | most common band, 12.03% of days |
| Min | 0.270x | smallest day observed |
| Max | 3.244x | largest day observed |
| P10 | 0.584x | very quiet day threshold |
| P25 | 0.738x | lower quartile |
| P75 | 1.192x | upper quartile |
| P90 | 1.501x | wide day threshold |
| P95 | 1.718x | extended day |
| P99 | 2.205x | outlier |

---

## Size Bucket Distribution

| Bucket | N Days | % of Days |
|--------|--------|-----------|
| Quiet (<0.6x) | 564 | 11.61% |
| Small (0.6-0.8x) | 1,022 | 21.05% |
| Normal (0.8-1.2x) | 2,089 | 43.02% |
| Large (1.2-1.5x) | 695 | 14.31% |
| Big (1.5-2.0x) | 395 | 8.13% |
| Outlier (>=2.0x) | 91 | 1.87% |

---

## Full Distribution -- 0.1x ABR Bins

| Band (xABR) | Count | % of Days | Cumulative % |
|-------------|-------|-----------|--------------|
| 0.2-0.3 | 2 | 0.04% | 0.04% |
| 0.3-0.4 | 40 | 0.82% | 0.86% |
| 0.4-0.5 | 190 | 3.91% | 4.78% |
| 0.5-0.6 | 333 | 6.86% | 11.64% |
| 0.6-0.7 | 437 | 9.00% | 20.63% |
| 0.7-0.8 | 584 | 12.03% | 32.66% |
| 0.8-0.9 | 576 | 11.86% | 44.52% |
| 0.9-1.0 | 572 | 11.78% | 56.30% |
| 1.0-1.1 | 533 | 10.98% | 67.28% |
| 1.1-1.2 | 410 | 8.44% | 75.72% |
| 1.2-1.3 | 302 | 6.22% | 81.94% |
| 1.3-1.4 | 241 | 4.96% | 86.90% |
| 1.4-1.5 | 150 | 3.09% | 89.99% |
| 1.5-1.6 | 133 | 2.74% | 92.73% |
| 1.6-1.7 | 92 | 1.89% | 94.63% |
| 1.7-1.8 | 68 | 1.40% | 96.03% |
| 1.8-1.9 | 51 | 1.05% | 97.08% |
| 1.9-2.0 | 51 | 1.05% | 98.13% |
| 2.0-2.1 | 22 | 0.45% | 98.58% |
| 2.1-2.2 | 19 | 0.39% | 98.97% |
| 2.2-2.3 | 10 | 0.21% | 99.18% |
| 2.3-2.4 | 11 | 0.23% | 99.40% |
| 2.4-2.5 | 11 | 0.23% | 99.63% |
| 2.5-2.6 | 1 | 0.02% | 99.65% |
| 2.6-2.7 | 7 | 0.14% | 99.79% |
| 2.7-2.8 | 3 | 0.06% | 99.86% |
| 2.8-2.9 | 2 | 0.04% | 99.90% |
| 2.9-3.0 | 3 | 0.06% | 99.96% |
| 3.0-3.1 | 1 | 0.02% | 99.98% |
| 3.2-3.3 | 1 | 0.02% | 100.00% |

---

## Key Observations

1. **Right-skewed distribution.** Mode (0.7-0.8x) sits below the mean (1.00x). Mean > median is the signature of right skew -- the tail of large days pulls the average up.

2. **One-third of days finish below 0.8x ABR** (32.66% cumulative). Quiet sessions are common, not exceptional.

3. **Half of all days fall between 0.74x and 1.19x ABR** (P25 to P75). Tight middle of the distribution.

4. **Sharp drop after 1.2x.** % of days falls from 10.98% (1.0-1.1x) and 8.44% (1.1-1.2x) down to 6.22% (1.2-1.3x). 1.2x is where extended days start being notably rarer.

5. **Fat right tail.** 10% of days exceed 1.5x ABR. 4% exceed 1.8x. 1.4% exceed 2.2x. Max observed is 3.24x.

6. **2x+ ABR days are rare but persistent.** 1.87% of days (n=91 across 19 years) -- roughly one every 7-8 weeks.

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v1.0 | 20260512 | Initial release. Daily range distribution at 0.1x ABR resolution. 4,856 FDAX daily bars from 2007-03-13 to 2026-05-11. |
