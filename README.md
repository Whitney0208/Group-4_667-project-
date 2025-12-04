````markdown
# Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes

[![Course](https://img.shields.io/badge/Course-BIOS%20667-blue)](https://www.google.com/search?q=BIOS+667)
[![Language](https://img.shields.io/badge/Language-R_%7C_Quarto-blue)](https://www.r-project.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success)]()
[![License](https://img.shields.io/badge/License-MIT-green)]()

> **A longitudinal analysis project comparing marginal GLMs and Random-Slope GLMMs to assess readmission risks under different insulin regimens.**

---

## 📑 Table of Contents
- [Project Overview](#-project-overview)
- [Key Findings](#-key-findings)
- [Repository Structure](#-repository-structure)
- [Methodology](#-methodology)
- [Reproducing the Analysis](#-reproducing-the-analysis)
- [Authors](#-authors)

---

## 📖 Project Overview

This repository contains the full analysis and report for a longitudinal study of 30-day hospital readmission among adults with diabetes. Utilizing encounter-level Electronic Health Record (EHR) data from **1,488 unique patients** contributing **4,160 encounters**, this project aims to disentangle the complex relationship between insulin treatment regimens and readmission trajectories.

**Core Objectives:**
* **Construct** a longitudinal cohort with multiple inpatient encounters per patient.
* **Quantify** the evolution of 30-day readmission risk over repeated encounters.
* **Compare** statistical strategies: Marginal Logistic GLM vs. Generalized Linear Mixed Models (GLMM).
* **Interpret** subject-specific heterogeneity using Random-Slope models.

---

## 📊 Key Findings

| Insulin Regimen | Readmission Trajectory |
| :--- | :--- |
| **No Insulin** | Risk **declines substantially** with successive encounters (Learning effect). |
| **Insulin Up** | Risk starts higher and **decreases significantly slower** (Flatter trajectory). |

**Statistical Insights:**
* **Heterogeneity:** Approximately **11%** of the variability in readmission risk is attributable to between-patient heterogeneity (ICC ≈ 0.11).
* **Model Selection:** The **Random-Slope GLMM** (with Insulin × Time interaction) provided the best fit compared to Random-Intercept only and Marginal GLMs.
* **Robustness:** Conditional and approximate marginal odds ratios (via Zeger’s method) yielded consistent conclusions.

---

## 📂 Repository Structure

The project files are organized as follows:

```text
├── 📄 Longitudinal...Diabetes.qmd   # Main Quarto source (Code + Narrative)
├── 📄 Longitudinal...Diabetes.pdf   # Final compiled Report (Best for reading)
├── 📄 Longitudinal...Diabetes.html  # Interactive HTML version
├── 💾 cleaned_diabetes....csv  # Analysis-ready dataset (Encounter level)
├── 💾 diabetic_data.csv             # Raw dataset (For reproducibility)
└── 📝 variable_definitions_table.csv# Data Dictionary
````

### Data Dictionary Highlights

| Variable | Description |
| :--- | :--- |
| `readmit30` | **Outcome**: 1 = readmitted within 30 days, 0 = otherwise. |
| `insulin` | **Exposure**: Insulin regimen (No, Steady, Up, Down). |
| `encounter_index` | **Time**: Truncated encounter index (1–5). |
| `Covariates` | Age, gender, race, admission type, LOS, prior utilization. |

-----

## 🧮 Methodology

We employed a rigorous comparative modeling strategy to handle correlated binary outcomes:

```mermaid
graph TD
    A[Raw Data] --> B(Data Cleaning & Cohort Construction)
    B --> C{Modeling Strategy}
    
    C --> D[Marginal Logistic GLM]
    D --> D1[Independence Working Model]
    D --> D2[Robust Sandwich SEs]
    
    C --> E[GLMMs]
    E --> E1[Random Intercept]
    E --> E2[Random Slope (Final Model)]
    
    D2 --> F[Compare & Interpret]
    E2 --> F
    F --> G[Final Inference]
```

1.  **Marginal Approach:** Modeled population-averaged effects using GEE-style robust standard errors.
2.  **Mixed-Effects Approach:** Modeled subject-specific trajectories, testing for random slopes to capture individual variation in recovery rates.

-----

## 💻 Reproducing the Analysis

### 1\. Prerequisites

Ensure you have **R (≥ 4.3)** and **Quarto (≥ 1.3)** installed.

### 2\. Install Dependencies

Run the following R code to install all necessary packages used in the `.qmd` file:

```r
packages <- c(
  "tidyverse", "broom", "broom.mixed", "car", "sandwich", "lmtest",
  "ResourceSelection", "pROC", "performance", "lme4", "geepack",
  "knitr", "kableExtra", "gridExtra", "scales"
)
install.packages(setdiff(packages, installed.packages()[, "Package"]))
```

### 3\. Render the Report

To regenerate the analysis from scratch, run the following command in your terminal:

```bash
quarto render "Longitudinal Modeling of 30-Day Hospital Readmission Among Adults With Diabetes.qmd"
```

-----

## 👥 Authors

**BIOS 667 Group 4**

  * **Zhangziyan Jiang**
  * **Wanbing Wang**
  * **Xiaochen Zhou**
  * **Muyao Tang**
  * **Danni Liu**

-----

*This project was conducted as part of the BIOS 667 (Generalized Linear Models) course.*

```