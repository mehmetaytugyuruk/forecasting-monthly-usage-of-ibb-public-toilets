# Forecasting Monthly Usage of İBB Public Toilets

This repository contains the research paper and full analysis pipeline for a data science study on **forecasting monthly public toilet usage** operated by the Istanbul Metropolitan Municipality (İBB).

The study formulates the problem as a **global multi-station time series regression task**, where a single model learns demand patterns across multiple locations.

---

## Paper

**Title:** Forecasting Monthly Usage of İBB Public Toilets Using a Single Global Model  
**Author:** Mehmet Aytuğ Yürük  
**Institution:** Istanbul University  
**Date:** January 2026  

The full paper is available in this repository as:

- `ibb.pdf`

---

## Problem Overview

Accurate demand forecasting is essential for efficient urban public services such as staffing, cleaning schedules, and resource allocation.

This work focuses on:
- Monthly usage demand of public toilets
- 26 stations with consistent historical records
- A five-year administrative dataset (2020–2024)

To avoid distortions caused by the COVID-19 period:
- 2020 data is excluded
- 2021 data is used only for lag feature construction
- The model is trained on 2022–2023 and tested on 2024

---

## Methodology

- **Model type:** Global forecasting model (single model for all stations)
- **Algorithm:** CatBoost Regressor
- **Features:**
  - Short-term and annual lag features
  - Rolling statistics (mean, volatility)
  - Momentum and relative change features
  - Cyclical month encoding (sin / cos)
- **Evaluation:** Rolling one-step-ahead forecasting (operationally realistic)

The global modeling approach replaces multiple station-specific models with a **single scalable artifact**.

---

## Results Summary

The CatBoost global model outperforms transparent baseline methods, including:
- Seasonal Naive (lag-12)
- Rolling Mean (lag-3)
- Hybrid baseline

Evaluation is performed using MAE and RMSE on the 2024 test period.

---

## Interpretability

Model behavior is analyzed using **SHAP**:
- Lag-based features are the dominant predictors
- Seasonal structure and short-term dynamics drive demand
- Station identity captures location-specific behavior

---

## Code

The full analysis and modeling pipeline is available in this repository:

- `main.ipynb` — data loading, exploratory analysis, feature engineering, baseline models, CatBoost training, and SHAP-based evaluation
- `ibb_2020_2025.csv` — the underlying dataset
- `figures/` — exported plots referenced in the paper

---

## Notes

- Dataset source: İBB Open Data Portal
- This study uses **endogenous signals only** (no external variables such as weather or events)
- Designed as a strong baseline for future exogenous extensions
