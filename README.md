# SAPM Monte Carlo — Pharmacy Benefit Management / Spread Extraction Trap

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Pharmacy Benefit Management (Spread Extraction Trap).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **6.35** |
| β_W mean | 6.46 |
| β_W std | 1.09 |
| **90% CI** | **[4.9, 8.4]** |
| 99% CI | [4.4, 9.5] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$381.0B/yr** |
| Π (revenue) | $60.0B/yr |

**β_W = 6.35** means the pharmacy benefit management industry destroys **$6.35 in system
welfare for every $1.00 in revenue** — across 5 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-pbm.git
cd sapm-mc-pbm
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 6.35` and `ΔW median : $381.0B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_spread_extraction | $151.0B | [$91.5B, $248.4B] | Lognormal |
| C2_patient_cost_shifting | $94.5B | [$75.6B, $113.4B] | Normal |
| C3_pharmacy_consolidation | $75.6B | [$60.5B, $90.7B] | Normal |
| C4_rebate_distortion | $37.8B | [$22.9B, $62.4B] | Lognormal |
| C5_regulatory_opacity | $18.9B | [$11.4B, $31.2B] | Lognormal |
| **Total ΔW** | **$381.0B** | **[$292.9B, $505.3B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.5 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0050%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Pharmacy Benefit Management (Spread Extraction Trap)*.
> GitHub: epostnieks/sapm-mc-pbm.
> https://github.com/epostnieks/sapm-mc-pbm
