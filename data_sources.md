# Data Sources — Pharmacy Benefit Management Monte Carlo Simulation

Channel parameters in `mc_simulation.py` trace to the sources listed here.
The paper (Pharmacy Benefit Management: Spread Extraction Trap) is available on SSRN and contains the full
reference list and §4 calibration narrative.

---

## Channel Sources

### `C1_spread_extraction`

PBM spread pricing $30-50B/yr in opaque spreads. Sources: FTC 2024, PCMA.

*Full citations: paper §4 (available SSRN).*

### `C2_patient_cost_shifting`

Copay clawbacks, formulary steering. Sources: NCPA, CMS.

*Full citations: paper §4 (available SSRN).*

### `C3_pharmacy_consolidation`

Independent pharmacy closures, pharmacy deserts. Sources: NCPA census, FTC.

*Full citations: paper §4 (available SSRN).*

### `C4_rebate_distortion`

Rebate bias against generics/biosimilars. Sources: IQVIA, Biosimilars Forum.

*Full citations: paper §4 (available SSRN).*

### `C5_regulatory_opacity`

ERISA preemption, no fiduciary duty. Sources: FTC, state AG investigations.

*Full citations: paper §4 (available SSRN).*

---

## Industry Revenue (Π)

The private payoff Π = $60.0B/yr is global annual industry revenue.
Source: paper §2 and §4. See paper §DA-1 (Decision Audit Field 7) for full
revenue source documentation.

---

## SAPM Framework

- Postnieks, E. (2026). *The Private Pareto Theorem*. SAPM Foundation Paper. SSRN.
- Postnieks, E. (2026). *Pharmacy Benefit Management (Spread Extraction Trap)*. SAPM Working Paper. SSRN.

---

## Distribution Methodology

- Iman, R. L., & Conover, W. J. (1982). A distribution-free approach to
  inducing rank correlation among input variables. *Communications in
  Statistics — Simulation and Computation*, 11(3), 311–334.
- Cooke, R. M. (1991). *Experts in Uncertainty*. Oxford University Press.
