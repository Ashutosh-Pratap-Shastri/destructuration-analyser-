# Probabilistic Destructuration Analyser — Structured Clays

Interactive Monte Carlo sensitivity tool exploring progressive bond
degradation in fissured high-plasticity clays under cyclic suction
(wetting–drying) loading.

**Live tool:** https://ashutosh-pratap-shastri.github.io/destructuration-analyser-/

## Scientific basis

The tool is **inspired by** the destructuration concept of the S-CLAY1S
constitutive model (Karstunen et al., 2005), which extends S-CLAY1
(Wheeler et al., 2003). In S-CLAY1S, the bonding variable degrades with
accumulated plastic volumetric and deviatoric strain.

This tool does **not** implement S-CLAY1S itself. It uses a simplified,
phenomenological per-cycle rule in which the plastic strain increment of
one wetting–drying cycle is driven by the suction amplitude, amplified by
fissure density and reduced by overconsolidation:

    Δb = −ξ · b · η · (Δs / (p_ref + s0)) · OCR^(−κs)

with p_ref = 100 kPa, s0 = 50 kPa and κs = 0.3. A sample is counted as
fully destructured when b ≤ 0.05.

## Uncertain parameters (5)

| Parameter | Symbol | Distribution in the Monte Carlo |
|---|---|---|
| Initial bond index | b₀ | Beta(2,2) on 0.5–1.0 |
| Fissure density | η | Lognormal, mean = slider value (0.01–0.20), CoV 0.25 |
| Overconsolidation ratio | OCR | Lognormal, mean = slider value (2–30), CoV 0.15 |
| Cyclic suction amplitude | Δs (kPa) | Normal truncated at 0, mean = slider value (10–200), CoV 0.20 |
| Degradation rate | ξ | Lognormal, mean 10, CoV 0.30 |

The sliders set the mean values of η, OCR and Δs; b₀ and ξ are sampled
around fixed values.

## Outputs

- Probability of full destructuration versus number of wetting–drying cycles (up to 50)
- Spearman rank correlation of each parameter with the cycle at which
  destructuration occurs (tornado chart; red = brings it earlier, blue = delays it)
- Summary: P(destructuration within 50 cycles), median cycle, most influential parameter

## Monte Carlo setup

- N = 1000 samples per run, maximum 50 cycles
- Samples that do not destructure within 50 cycles are assigned cycle 51 (censored)

## Limitations

- Exploratory sensitivity tool; the degradation rule is phenomenological and
  its constants are illustrative, not calibrated against laboratory data.
- Parameters are sampled independently (no correlation between them).
- No coupling to a stress–strain model: only the bond index is tracked.

## References

- Wheeler, S.J., Näätänen, A., Karstunen, M. & Lojander, M. (2003). An anisotropic elastoplastic model for soft clays. *Canadian Geotechnical Journal*, 40(2), 403–418.
- Karstunen, M., Krenn, H., Wheeler, S.J., Koskinen, M. & Zentar, R. (2005). Effect of anisotropy and destructuration on the behavior of Murro test embankment. *International Journal of Geomechanics*, 5(2), 87–97. https://doi.org/10.1061/(ASCE)1532-3641(2005)5:2(87)
