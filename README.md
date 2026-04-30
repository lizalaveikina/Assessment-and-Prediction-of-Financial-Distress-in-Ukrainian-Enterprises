# Assessment and Prediction of Financial Distress in Ukrainian Enterprises

## Abstract

This study examines financial distress prediction among Ukrainian enterprises across two major economic shocks: the COVID-19 pandemic (2020) and the full-scale war (2022). Using a panel dataset of **81,269 firm-year observations** across **18,183 unique firms** covering **2018 to 2024**, the study applies pooled logistic regression and a Random Forest classifier to identify the key determinants of financial distress. The Random Forest outperforms logistic regression, particularly in recall, driven by nonlinear threshold effects in the leverage-distress relationship. Operating profitability and total leverage emerge as the dominant predictors across all industries and crisis periods. The analysis further examines distress persistence, industry heterogeneity in distress determinants, and how predictive signals shift between the two crises. Results carry practical implications for creditors, firm managers, and financial regulators operating in crisis-prone environments.

## Data Availability

The data used in this study are provided by [**YouControl**](https://youcontrol.com.ua) and contain confidential firm-level financial statements of Ukrainian enterprises. Due to confidentiality constraints, the raw data files are not included in this repository. The `data/` folder contains a description of the dataset structure, variable definitions, and the composite distress proxy construction.

## Reproducibility Note

The notebooks are provided for transparency and documentation of the analytical pipeline. However, **running the notebooks locally will not reproduce the results** as the underlying data files are not publicly available. The code is intended to fully document the methodology, variable construction, and modelling choices described in the thesis. 
