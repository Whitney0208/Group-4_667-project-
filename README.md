# Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Quarto](https://img.shields.io/badge/Tool-Quarto-blueviolet.svg)
![Status](https://img.shields.io/badge/Status-Complete-green.svg)

**Authors:** Zhangziyan Jiang, Wanbing Wang, Xiaochen Zhou, Muyao Tang, Danni Liu

---

## 📖 Project Overview

This repository contains a comprehensive longitudinal analysis of **30‑day hospital readmission** among adults with diabetes. Leveraging electronic health records (EHR), this project investigates how readmission risk evolves across repeated hospital encounters and quantifies the impact of different insulin regimens on patient recovery trajectories.

### 🎯 Key Research Questions
1.  **Temporal Evolution:** How does the risk of 30‑day readmission change with successive hospital encounters?
2.  **Treatment Interaction:** Do readmission trajectories differ by insulin regimen (No insulin, Steady dose, Up‑titration, Down‑titration)?
3.  **Variance Decomposition:** How much of the variability in readmission risk is attributable to between‑patient heterogeneity versus within‑patient temporal changes?

---

## 📂 Repository Structure

Based on the current file directory, the repository is organized as follows:

| File Name | Description |
| :--- | :--- |
| `Longitudinal Modeling...qmd` | **Main Analysis Source Code.** A Quarto document containing data processing, GLM/GLMM modeling, diagnostics, and narrative text. |
| `Longitudinal Modeling...pdf` | **Full Report (PDF).** The typeset final report generated from the analysis. |
| `Longitudinal Modeling...html` | **Web Report (HTML).** Interactive version of the final report. |
| `cleaned_diabetes_longitudinal.csv` | **Analysis-Ready Data.** Longitudinal dataset at the encounter level used for all models. |
| `diabetic_data.csv` | **Raw Data.** The original dataset from which the cleaned file was derived. |
| `variable_definitions_table.csv` | **Data Dictionary.** Definitions and coding schemas for variables used in the analysis. |

---

## 📊 Methodology

The analysis employs a hierarchical modeling strategy to handle correlated data (repeated measures within patients):

1.  **Marginal Logistic GLM:** * Establishes population-averaged associations.
    * Uses Cluster-Robust Standard Errors (Sandwich Estimator) to account for patient-level clustering.
2.  **Generalized Linear Mixed Models (GLMM):**
    * **Random Intercept:** Accounts for baseline heterogeneity in patient frailty.
    * **Random Slope:** Allows the rate of recovery (time effect) to vary by patient.
    * **Primary Model:** A random-slope GLMM including an `Insulin × Time` interaction term.

**Statistical Stack:**
* **Language:** R
* **Framework:** Quarto
* **Key Libraries:** `lme4`, `geepack`, `tidyverse`, `pROC`, `performance`, `broom.mixed`.

---

## 📉 Key Findings

* **Learning Effect:** Among patients *not* on insulin, readmission risk declines significantly over successive encounters.
* **The "Insulin Up" Phenotype:** Patients undergoing insulin intensification start at a higher baseline risk and experience a **significantly slower decline** in risk over time compared to non-insulin patients.
* **Patient Heterogeneity:** The random-slope model revealed that approximately **11%** of the variability in readmission risk is attributable to unobserved between-patient differences (ICC $\approx$ 0.113).

---

## 🛠️ How to Reproduce

To regenerate the analysis and reports locally:

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    ```
2.  **Install Dependencies:**
    Ensure you have R installed along with the required packages (listed in the `.qmd` file).
3.  **Render the Report:**
    Run the following command in your terminal or RStudio console:
    ```bash
    quarto render "Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.qmd"
    ```

---

## 📝 Data Dictionary

A brief overview of key variables in `cleaned_diabetes_longitudinal.csv`:

* **`patient_nbr`**: Unique patient identifier.
* **`readmit30`**: Binary outcome (1 = Readmitted within 30 days, 0 = No).
* **`encounter_index`**: Sequential order of the hospital visit.
* **`insulin`**: Regimen category (No, Steady, Down, Up).
* **`encounter_index_trunc`**: Encounter index capped at 5 to handle sparsity.

---

## 📧 Contact

For questions regarding the methodology or data processing, please contact the authors listed above.