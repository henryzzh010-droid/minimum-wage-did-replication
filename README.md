# Minimum Wage DID Replication & Extension

## Project Overview

This project replicates and extends the analysis of Card and Krueger (1994), which examines the impact of a minimum wage increase on employment in the fast-food industry. The study compares fast-food restaurants in New Jersey (treatment group) and Pennsylvania (control group) before and after the 1992 minimum wage increase.

The main research question is:

> Does the increase in minimum wage in New Jersey affect employment in fast-food restaurants?

---

## Methodology

### Baseline Difference-in-Differences (DID)

The baseline model estimates the causal effect of the minimum wage increase using a Difference-in-Differences (DID) framework:

Y = β₀ + β₁ treated + β₂ post + β₃ (treated × post) + ε

* **treated**: indicator for New Jersey (treatment group)
* **post**: indicator for post-policy period
* **did**: interaction term (treated × post), capturing the treatment effect

The dependent variable is **full-time equivalent employment (fte)**, constructed as:

fte = EMPFT + 0.5 × EMPPT + NMGRS

---

## Data

The dataset contains store-level observations from fast-food restaurants in New Jersey and Pennsylvania. Key variables include:

* Employment: EMPFT, EMPPT, NMGRS
* Prices: PSODA, PFRY, PENTREE
* Store characteristics: CHAIN, CO_OWNED
* Treatment indicators: treated, post, did

---

## Phase 1: Data Preparation

* Loaded raw dataset and verified structure
* Cleaned variables and handled missing values
* Constructed the **fte** variable
* Exported cleaned dataset:

```
data/processed/njmin_panel_clean.csv
```

---

## Phase 2: Replication

### 1. Descriptive Statistics

Summary statistics were computed to understand the distribution of key variables.

### 2. Difference-in-Means

Calculated mean employment differences across groups and time periods.

### 3. DID Estimation

Estimated the baseline DID model using OLS with robust standard errors.

### 4. Clustered Standard Errors

Extended the model by clustering standard errors at the store level.

Outputs:

```
data/processed/table2_descriptive.csv
data/processed/did_cluster_results.csv
```

---

## Phase 3: Extension

### Extension Strategy

The baseline DID approach relies on the parallel trends assumption without explicitly validating it. To improve robustness, this project extends the analysis by incorporating store-level control variables.

### Extended Model

fte = β₀ + β₁ treated + β₂ post + β₃ did + β₄ controls + ε

Controls include:

* CHAIN (restaurant chain)
* CO_OWNED (ownership type)
* NREGS (store size proxy)

### Results

The estimated DID coefficient remains positive and statistically insignificant, suggesting that the minimum wage increase did not reduce employment.

Including control variables improves the robustness of the results by accounting for observable differences across stores.

---

## Visualization

A coefficient plot with 95% confidence intervals is generated to visualize the estimated effects:

```
data/processed/extension_coefficient_plot.png
```

---

## Key Findings

* The minimum wage increase in New Jersey did **not reduce employment** in fast-food restaurants
* Results are consistent across baseline and extended models
* Adding control variables does not change the overall conclusion

---

## Repository Structure

```
minimum-wage-did-replication/
├── README.md
├── data/
│   ├── raw/
│   └── processed/
│       ├── njmin_panel_clean.csv
│       ├── table2_descriptive.csv
│       ├── did_cluster_results.csv
│       ├── extension_results.csv
│       └── extension_coefficient_plot.png
└── notebooks/
    ├── 01_Data_Cleaning.ipynb
    ├── 02_Replication.ipynb
    └── 03_Extension_and_Results.ipynb
```

---

## Conclusion

This project replicates the core findings of Card and Krueger (1994) and extends the analysis by incorporating store-level controls. The results consistently show no evidence that the minimum wage increase reduced employment, supporting the original conclusion.

---
