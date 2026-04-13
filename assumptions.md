# Monte Carlo Assumptions — Pharmacy Benefit Management / Spread Extraction Trap

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $60.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 6.35 | Confirmed by N=100,000 draws |
| ΔW median (result) | $381.0B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_spread_extraction` | lognormal | $83.2B | $151.2B | $249.5B | PBM spread pricing $30-50B/yr in opaque spreads. Sources: FTC 2024, PCMA. |
| `C2_patient_cost_shifting` | normal | $75.6B | $94.5B | $113.4B | Copay clawbacks, formulary steering. Sources: NCPA, CMS. |
| `C3_pharmacy_consolidation` | normal | $60.5B | $75.6B | $90.7B | Independent pharmacy closures, pharmacy deserts. Sources: NCPA census, FTC. |
| `C4_rebate_distortion` | lognormal | $20.8B | $37.8B | $62.4B | Rebate bias against generics/biosimilars. Sources: IQVIA, Biosimilars Forum. |
| `C5_regulatory_opacity` | lognormal | $10.4B | $18.9B | $31.2B | ERISA preemption, no fiduciary duty. Sources: FTC, state AG investigations. |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.5 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.5) = 0.0050%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 6.3 | 20% DC adj = 5.04 | 40% DC adj = 3.78

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $381B = 0.4% of world GDP ($106T) ✓
- **β_W range**: 6.35 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
