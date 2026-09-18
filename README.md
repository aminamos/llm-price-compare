# LLM Price Compare

Per-token API pricing by provider vs coding benchmark score. Same model can
appear once per provider because pricing differs by route. Ranked by
benchmark score, highest first.

Last verified: 2026-09-18. Prices in USD per 1M tokens.

## Ranked table

Benchmark column is Terminal-Bench 2.1 (the one coding benchmark with a
published score for all ranked models). Blended overall = 0.75 x input
(cache miss, off-peak where applicable) + 0.25 x output.

| Rank | Model | Provider | In $/1M | Out $/1M | Cache hit $/1M | Cache miss $/1M | Peak rates | Off-peak rates | Blended $/1M | Terminal-Bench 2.1 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Muse Spark 1.3 (standard) | Meta | 1.25 | 4.25 | 0.15 | 1.25 | flat | flat | 2.00 | 88.8 |
| 2 | DeepSeek V4 Flash (0731) | DeepSeek official | 0.22 | 0.66 | 0.007 | 0.22 | 0.44 in / 1.32 out / 0.014 hit | 0.22 in / 0.66 out / 0.007 hit | 0.33 | 82.7 |
| 2 | DeepSeek V4 Flash (0731) | Sference | 0.28 | 0.56 | 0.07 | 0.28 | flat | flat | 0.35 | 82.7 |
| 3 | MiniMax M3 | MiniMax | 0.30 | 1.20 | 0.06 | 0.30 | flat | flat | 0.525 | 66.0 |

## Unranked (no Terminal-Bench 2.1 score yet)

| Model | Provider | In $/1M | Out $/1M | Cache hit $/1M | Cache miss $/1M | Peak rates | Off-peak rates | Blended $/1M |
|---|---|---|---|---|---|---|---|---|
| DeepSeek V4.1 Flash | Sference | 0.50 | 1.50 | 0.05 | 0.50 | flat | flat | 0.75 |
| GLM 5.3 | Sference | 1.20 | 4.20 | 0.26 | 1.20 | flat | flat | 1.95 |
| GLM 5.2 (alias of 5.3) | Sference | 1.20 | 4.20 | 0.26 | 1.20 | flat | flat | 1.95 |
| GLM 5.3 Flash | Sference | 0.20 | 0.60 | 0.07 | 0.20 | flat | flat | 0.30 |
| Kimi K3 | Sference | 3.00 | 15.00 | 0.45 | 3.00 | flat | flat | 6.00 |

## Notes

- Muse Spark 1.3: standard tier. Contributor tier ($0.10 in / $0.20 out,
  Meta trains on your data) excluded by request. The 88.8 score is the
  `max` reasoning variant (limited preview); the score of the generally
  available `xhigh` API variant on this benchmark is undisclosed.
- DeepSeek V4 Flash official: 0731 release. Peak = weekdays 01:00-04:00
  and 06:00-10:00 UTC; weekends off-peak all day. Sference lists the same
  checkpoint at flat $0.28 / $0.56 / $0.07 with no peak schedule.
- MiniMax M3: per-token API route via MiniMax. Separately, the Token Plan
  subscription is Plus $22/mo (~1.7B M3 tokens), Max $55/mo (~5.1B),
  Ultra $132/mo (~12.5B) - shared multimodal quota, not per-token billing.
- All benchmark scores are vendor-reported with different harnesses, so
  the ranking is indicative, not a controlled comparison. See
  `benchmark-llms` for independent SWE-bench runs.

## Sources

- Muse Spark 1.3 pricing: Vercel AI Gateway changelog 2026-09-02
  (meta/muse-spark-1.3 $1.25 / $4.25 / $0.15 cached).
- Muse Spark 1.3 benchmarks: Artificial Analysis 2026-09-02
  (Intelligence Index 61 xhigh / 62 max; Terminal-Bench 2.1 88.8 max).
- DeepSeek official pricing: official docs, re-verified 2026-09-03
  (off-peak $0.007 hit / $0.22 miss / $0.66 out; peak 2x).
- DeepSeek V4 Flash benchmarks: official model card via NVIDIA Build
  (SWE Verified Max 79.0); 0731 release card (Terminal-Bench 2.1 82.7).
- MiniMax M3 pricing: LLMReference provider ladder
  (MiniMax route $0.30 / $1.20 / $0.06 cache read); Token Plan page.
- MiniMax M3 benchmarks: official model card via Hugging Face
  (SWE-bench Verified 80.5; Terminal-Bench 2.1 66.0).
- Sference rows: Sference serverless catalog snapshot 2026-09-18
  (user-provided; flat rates, unlimited TPM/RPM, 1M context).

Machine-readable: `prices.csv`.
