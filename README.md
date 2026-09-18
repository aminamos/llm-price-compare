# LLM Price Compare

Per-token API pricing by provider vs coding benchmark score. Same model can
appear once per provider because pricing differs by route. Ranked by
blended benchmark score, highest first.

Last verified: 2026-09-18. Prices in USD per 1M tokens.

## Ranked table

Benchmark columns are Terminal-Bench 2.1, DeepSWE v1.1, SWE-bench Verified,
SWE-bench Pro. Blended = mean of available scores (n varies, shown in
parentheses). Rank is top-down by blended. Blended overall price = 0.75 x
input (cache miss, off-peak where applicable) + 0.25 x output.

| Rank | Model | Provider | In $/1M | Out $/1M | Cache hit $/1M | Cache miss $/1M | Peak rates | Off-peak rates | Blended $/1M | TB-2.1 | DeepSWE | SWE-Ver | SWE-Pro | Blend (n) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | DeepSeek V4.1 Flash (effort max) | Sference | 0.50 | 1.50 | 0.05 | 0.50 | flat | flat | 0.75 | 90.6 | 74.2 | - | - | 82.4 (2) |
| 1 | DeepSeek V4.1 Flash (effort max) | DeepInfra | 0.20 | 0.60 | 0.006 | 0.20 | flat | flat | 0.30 | 90.6 | 74.2 | - | - | 82.4 (2) |
| 2 | Muse Spark 1.3 max (standard) | Meta | 1.25 | 4.25 | 0.15 | 1.25 | flat | flat | 2.00 | 88.8 | 75.4 | - | - | 82.1 (2) |
| - | Muse Spark 1.3 xhigh (standard) | Meta | 1.25 | 4.25 | 0.15 | 1.25 | flat | flat | 2.00 | 85† | - | - | - | 85.0 (1)† |
| 3 | MiniMax M3 | MiniMax | 0.30 | 1.20 | 0.06 | 0.30 | flat | flat | 0.525 | 66.0 | - | 80.5 | 59.0 | 68.5 (3) |

† Single-score row (n=1), different harness from the vendor numbers, so it
carries no rank. Rank only compares multi-score blends.

## Unranked (no common benchmark score yet)

| Model | Provider | In $/1M | Out $/1M | Cache hit $/1M | Cache miss $/1M | Peak rates | Off-peak rates | Blended $/1M |
|---|---|---|---|---|---|---|---|---|
| GLM 5.3 | Sference | 1.20 | 4.20 | 0.26 | 1.20 | flat | flat | 1.95 |
| GLM 5.2 (alias of 5.3) | Sference | 1.20 | 4.20 | 0.26 | 1.20 | flat | flat | 1.95 |
| GLM 5.3 Flash | Sference | 0.20 | 0.60 | 0.07 | 0.20 | flat | flat | 0.30 |
| Kimi K3 | Sference | 3.00 | 15.00 | 0.45 | 3.00 | flat | flat | 6.00 |

## Notes

- Muse Spark 1.3: standard tier. Contributor tier ($0.10 in / $0.20 out,
  Meta trains on your data) excluded by request. The 88.8 score is the
  `max` reasoning variant (limited preview); the score of the generally
  available `xhigh` API variant on this benchmark is undisclosed.
- DeepSeek V4.1 Flash is the current generation; V4 Flash / Pro rows
  removed.
- MiniMax M3: per-token API route via MiniMax. Separately, the Token Plan
  subscription is Plus $22/mo (~1.7B M3 tokens), Max $55/mo (~5.1B),
  Ultra $132/mo (~12.5B) - shared multimodal quota, not per-token billing.
- Thinking levels are separate rows. V4.1 Flash supports effort 1-100;
  published scores are max effort only. Muse 1.3 max is vendor-reported;
  xhigh TB-2.1 85 is Artificial-Analysis-measured, xhigh DeepSWE is
  undisclosed. MiniMax M3 has no reasoning-effort dial, so one row.
- DeepInfra V4.1 Flash also offers Priority (1.5x) and Flex (0.8x) tiers;
  table shows standard tier.

## Sources

- Muse Spark 1.3 pricing: Vercel AI Gateway changelog 2026-09-02
  (meta/muse-spark-1.3 $1.25 / $4.25 / $0.15 cached).
- Muse Spark 1.3 benchmarks: Artificial Analysis 2026-09-02
  (Intelligence Index 61 xhigh / 62 max; Terminal-Bench 2.1 88.8 max).
- DeepSeek V4.1 Flash benchmarks: benchlm.ai model page, updated
  2026-09-14 (Terminal-Bench 2.1 90.6; DeepSWE 74.2); LM Studio model page
  and Fireworks 2026-09-14 cross-check (DeepSWE 74.34 on their scaffold).
- DeepSeek V4.1 Flash pricing: Sference catalog snapshot 2026-09-18;
  DeepInfra model page ($0.20 / $0.60 / $0.006 cached).
- MiniMax M3 pricing: LLMReference provider ladder
  (MiniMax route $0.30 / $1.20 / $0.06 cache read); Token Plan page.
- MiniMax M3 benchmarks: official model card via Hugging Face
  (SWE-bench Verified 80.5; Terminal-Bench 2.1 66.0).
- Sference rows: Sference serverless catalog snapshot 2026-09-18
  (user-provided; flat rates, unlimited TPM/RPM, 1M context).

Machine-readable: `prices.csv`.
