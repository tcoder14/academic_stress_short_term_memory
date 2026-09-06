# Academic Stress and Short-Term Memory: A Data Analysis Study

A quantitative research project testing whether academic stress relates to short-term memory performance in undergraduate students, and whether that relationship is linear or follows an inverted-U (Yerkes–Dodson) curve.

**TL;DR:** Simple correlation says "more stress, worse memory." Quadratic regression tells a richer story — performance peaks at moderate stress and drops off at both extremes, and the curved model explains far more variance (ΔR² up to +0.35) than the straight-line one.

## Research Question

Does academic stress predict short-term memory performance in undergraduate students, and is that relationship better described by a linear trend or an inverted-U curve?

## Repository Contents

| File | Description |
|---|---|
| `stress_digitspan_data.csv` | Raw dataset — 60 participants × 17 variables (demographics, 8 stress items, stress totals, digit-span outcomes) |
| `academic_stress_and_short_term_memory.ipynb` | Full analysis pipeline in Python: cleaning, EDA, correlation, quadratic regression, sensitivity analysis |
| `academic_stress_and_short_term_memory_report.pdf` | Full written report (APA-style: intro, methodology, results, discussion, limitations) |
| `academic_stress_and_short_term_memory_slides.pdf` | Slide summary of the study and findings |

## Dataset

- **N = 60** undergraduate participants (ages 23–25), convenience sample
- **Predictors:** an 8-item academic-stress questionnaire (summed score, range 8–40) and a single 0–10 current-stress rating taken immediately before the memory task
- **Outcome:** forward digit-span performance, measured two ways — highest span passed and total correct trials
- No missing values, no duplicate participant IDs

## Methods

- Descriptive statistics and data validation
- Pearson (+ Spearman as a robustness check) correlation between stress and memory outcomes
- Quadratic regression (centered linear term + squared term) to directly test for inverted-U curvature, rather than relying on a linear correlation that could mask a curved relationship
- Model comparison via ΔR² between linear and quadratic fits
- Cook's distance screening and exclude-and-rerun sensitivity checks for influential observations

**Stack:** `pandas`, `numpy`, `scipy.stats`, `statsmodels`, `matplotlib`

## Key Results

| Predictor → Outcome | Pearson r (p) | Quadratic R² (ΔR²) | Squared term b (p) |
|---|---|---|---|
| Academic stress → highest span | −0.346 (.007) | 0.351 (+0.231) | −0.0106 (<.001) |
| Academic stress → correct trials | −0.400 (.002) | 0.487 (+0.327) | −0.0222 (<.001) |
| Current stress → highest span | −0.427 (<.001) | 0.420 (+0.238) | −0.1217 (<.001) |
| Current stress → correct trials | −0.390 (.002) | 0.499 (+0.347) | −0.2584 (<.001) |

- All four squared terms were negative and significant — consistent with downward (inverted-U) curvature across both stress measures and both memory outcomes.
- The academic-stress model peaked around a stress score of ~22 (roughly the midpoint of the 8–40 scale).
- Results held after removing Cook's-distance-flagged outliers (quadratic R² for the primary model actually rose from 0.351 to 0.542).

## Limitations

Correlational, cross-sectional, convenience-sampled data from a single, narrow demographic (mostly 4th-year CSE students) — see the full report for a complete discussion of validity and generalizability constraints.

## Author

Hasan Al Tanzim — PSY101 (Intro to Psychology) university research project
