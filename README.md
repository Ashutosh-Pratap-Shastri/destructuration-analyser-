# Probabilistic Destructuration Analyser — Structured Clays

Interactive Monte Carlo sensitivity tool simulating progressive bond 
degradation in fissured high-plasticity clays under cyclic suction loading.

**Live tool:** https://ashutosh-pratap-shastri.github.io/destructuration-analyser-/

## Scientific Basis

Implements the bond degradation law from the S-CLAY1S constitutive 
framework (Karstunen et al., 2005), where the bond index b decays as:

    Δb = -ξ · b · Δεp

Plastic strain per cycle is driven by cyclic suction amplitude and 
amplified by fissure density, following hydro-mechanical fatigue logic 
for Palaeogene high-plasticity clays (Søvind Marl, Little Belt Clay).

## Inputs

| Parameter | Symbol | Range |
|---|---|---|
| Initial Bond Strength Index | b₀ | 0.5 – 1.0 |
| Fissure Density Parameter | η | 0.01 – 0.20 |
| Overconsolidation Ratio | OCR | 2 – 30 |
| Cyclic Suction Amplitude | Δs (kPa) | 10 – 200 |

## Outputs

- Cumulative probability of full destructuration vs. wetting-drying cycle number
- Spearman rank sensitivity tornado chart across all uncertain parameters
- Summary statistics: P(destructuration), median failure cycle, dominant parameter

## Monte Carlo Setup

- N = 1000 samples per run
- Parameters sampled from physically motivated distributions 
  (Beta, Lognormal, truncated Normal)
- Fully softened threshold: b ≤ 0.05
- Maximum cycles simulated: 50

## Relevance

Developed to support PhD research on micro-to-macro constitutive 
modelling of fissured stiff clays for climate-resilient infrastructure 
(Aarhus University CEBE programme context).
