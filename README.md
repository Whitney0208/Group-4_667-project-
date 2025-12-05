# Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes

**Authors:** Zhangziyan Jiang, Wanbing Wang, Xiaochen Zhou, Muyao Tang, Danni Liu

---

## Project Overview

This repository contains the code and report for a longitudinal analysis of 30‑day hospital readmission among adults with diabetes. Using encounter‑level electronic health record data, we study how readmission risk changes over repeated hospitalizations and how these trajectories differ across insulin regimens.

We focus on:

- How the risk of 30‑day readmission changes with encounter index.
- Whether time trends differ between insulin regimens (No, Steady, Up, Down).
- How much of the variation in readmission is explained by between‑patient heterogeneity.

---

## Repository Contents

| File | Description |
| :--- | :--- |
| `Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.qmd` | Quarto source for the full analysis (data processing, GLM/GEE/GLMM, figures, and text). |
| `Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.pdf` | Typeset report. |
| `Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.html` | HTML report. |
| `cleaned_diabetes_longitudinal_Nov29.csv` | Analysis dataset at the encounter level. |
| `diabetic_data.csv` | Original raw data. |
| `variable_definitions_table.csv` | Variable definitions and coding. |

---

## Methods (brief)

- Marginal logistic GLM with and without truncated encounter index, with patient‑level cluster‑robust standard errors.
- GEE with logit link and exchangeable working correlation, considering main‑effects and insulin×time mean structures.
- Logistic GLMMs with random intercepts and random slopes for encounter index, including an insulin×time interaction; model selection based on likelihood ratio tests and AIC.

Analyses are implemented in R via Quarto. Key packages include `tidyverse`, `lme4`, `geepack`, `sandwich`, `lmtest`, `pROC`, and `performance`.

---

## Main Conclusions

- For patients not treated with insulin, 30‑day readmission risk declines as encounter index increases.
- Patients with insulin intensification start at higher risk and show a flatter decline in readmission probability over time, even after adjustment for prior utilization and other covariates.
- Mixed‑effects models indicate that roughly 11% of the variability in readmission risk is due to between‑patient differences (intraclass correlation about 0.11), consistent with meaningful within‑patient correlation over time.
- Across the GLM with robust standard errors, GEE, and random‑slope GLMM, the estimated insulin‑by‑time interaction and conclusions about trajectory differences are similar. Discrimination is modest (AUC about 0.59), so the models are used for inference rather than individual‑level prediction.

---

## Reproducibility

To rerun the analysis:

1. Open the project in R with the working directory set to the repository root.
2. Install the R packages used in the `.qmd` file if needed.
3. Render the report, for example from RStudio using the Knit button, or from a terminal with Quarto installed:

```bash
quarto render "Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.qmd"
```
