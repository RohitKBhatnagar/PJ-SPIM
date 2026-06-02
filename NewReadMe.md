# SAT Performance and Socioeconomic Determinants (2019–2024)

State-level, multi-year analysis of SAT outcomes using socioeconomic and participation indicators from public U.S. datasets.

## Executive Summary
This project studies whether state SAT performance can be predicted from participation patterns and socioeconomic context.  
Across all modeling choices, participation rate is the strongest structural factor. Socioeconomic indicators matter, but much of their apparent effect depends on participation regime (broad testing vs selective testing).

Key result in plain terms:
- The model can predict SAT outcomes reasonably well overall.
- Predictions are much easier in low-participation states (more selective test-taking).
- After removing participation effects, very little additional predictable signal remains.

---

## Why This Project Matters (Layman Version)
Raw SAT averages can be misleading when one state tests almost everyone and another tests only a small college-bound group.  
So we built models to answer:  
- How much of SAT variation is about participation structure?  
- How much is about income, poverty, and educational attainment?  
- Which modeling approach is most reliable for this type of data?

---

## Data Sources
- College Board SAT state-level reports (2019–2024)
- U.S. Census ACS (DP02, DP03)
- NCES supporting education context files

Merged and cleaned analysis dataset:
- 255 state-year observations used for modeling
- Core predictors: participation rate, median income, poverty rate, bachelor’s attainment

---

## Method Overview
1. Build unified SAT + Census panel by state-year  
2. Run exploratory analysis and diagnostics  
3. Train baseline linear models  
4. Add cross-validated Ridge model for regularization  
5. Add Random Forest + hyperparameter tuning  
6. Add participation-aware segmented models  
7. Add residual modeling (control participation first)  
8. Add SHAP explainability and diagnostic plots

---

## Model Results Comparison

### Main Global Models (directly comparable)

| Model | RMSE | MAE | R² | Notes |
|---|---:|---:|---:|---|
| Baseline Linear Regression | 73.87 | 44.90 | 0.593 | Simple baseline |
| Ridge + GridSearchCV | 73.79 | 44.79 | 0.594 | Best alpha = 0.1 |
| Random Forest (initial) | 59.36 | 29.09 | 0.737 | Strong nonlinear fit |
| Random Forest + GridSearchCV | 59.68 | 29.97 | 0.735 | Best params below |

Best Random Forest params:
- max_depth: None
- min_samples_leaf: 2
- min_samples_split: 2
- n_estimators: 500

### Participation-Aware Segmented Models (different subsets)

| Segment Model | RMSE | MAE | R² | Records |
|---|---:|---:|---:|---:|
| High Participation | 39.44 | 30.31 | 0.613 | 99 |
| Low Participation | 27.82 | 21.49 | 0.871 | 156 |

### Residual Modeling (not directly comparable to above)
Residual target: SAT variation left after modeling participation first.

| Residual Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Random Forest on participation-controlled residuals | 63.23 | 37.42 | 0.015 |

---

## What These Metrics Mean (Simple)
- RMSE: Typical prediction error, but penalizes big misses more.
- MAE: Average prediction miss in SAT points.
- R²: Percent of score variation explained by the model.

Example:
- R² = 0.735 means about 73.5% of differences are explained by the model.
- MAE = 29.97 means the prediction is off by about 30 SAT points on average.

---

## Why We Ran Multiple Models (Layman Explanation)
- Linear Regression: Easy to interpret baseline.
- Ridge (cross-validated): Checks if regularization helps stability when predictors overlap.
- Random Forest: Captures nonlinear patterns and interactions.
- Participation-aware segmentation: Treats high vs low participation as structurally different systems.
- Residual modeling: Tests whether socioeconomic features add signal after participation is already explained.
- SHAP: Explains why the model made each prediction.

Bottom line:
- Participation is the dominant structural driver.
- Random Forest gives the best global predictive performance.
- Segmenting by participation greatly improves interpretability.
- After controlling participation first, very little predictable signal remains (R² near zero in residual model).

---

## Key Findings
- Participation rate strongly shapes observed SAT averages.
- Income and educational attainment are meaningful but collinear.
- Poverty contributes, but less than participation.
- Low-participation states are much easier to predict.
- High-participation states are more complex due to broader test-taking population.
- SHAP confirms model reliance patterns and improves transparency.

---

## Plot Gallery

## Core EDA and Relationship Plots
![SAT score distribution by year](plots/sat_score_distribution_by_year.png)
![Participation vs SAT](plots/participation_rate_vs_sat_scores.png)
![Income vs SAT](plots/income_vs_sat_scores.png)
![Correlation heatmap](plots/correlation_matrix_SAT_Socioeconomic_Features.png)
![VIF plot](plots/vif_socioeconomic_features.png)

## Modeling and Explainability Plots
![Random Forest feature importance](plots/rf_feature_importance.png)
![Ridge actual vs predicted](plots/ridge_actual_vs_predicted.png)
![Random Forest predicted vs actual](plots/rf_pred_vs_actual.png)
![Random Forest error vs participation](plots/rf_error_vs_participation.png)
![SHAP summary](plots/shap_summary_sat.png)

## Additional Plots Generated
![Residual plot](plots/residual_plot.png)
![Socioeconomic gap scatter](plots/socioeconomic_gap_scatter.png)
![Policy correlation heatmap](plots/final_policy_correlation_heatmap.png)
![Feature importance comparison](plots/final_feature_importance_comparison.png)
![Partial dependence top anchors](plots/partial_dependence_top_anchors.png)
![Participation vs SAT high participation subset](plots/participation_rate_vs_sat_scores_high_participation.png)

## SHAP Force Plots by State
All generated force plots are available in:
- shap_force_plots

Direct links:
- Alabama
- Alaska
- Arizona
- Arkansas
- California
- Colorado
- Connecticut
- Delaware
- District of Columbia
- Florida
- Hawaii
- Idaho
- Illinois
- Indiana
- Iowa
- Kansas
- Kentucky
- Louisiana
- Maine
- Maryland
- Michigan
- Minnesota
- Mississippi
- Missouri
- Montana
- Nebraska
- Nevada
- New Hampshire
- New Jersey
- New Mexico
- New York
- North Carolina
- North Dakota
- Ohio
- Oklahoma
- Oregon
- Pennsylvania
- Rhode Island
- South Carolina
- South Dakota
- Tennessee
- Texas
- Utah
- Vermont
- Virginia
- Washington
- West Virginia
- Wisconsin
- Wyoming

---

## Project Structure
- Notebook: CapStone_SAT.ipynb
- Data folder: data
- Plot outputs: plots
- SHAP force plots: shap_force_plots

---

## Final Conclusion (Layman)
If two states have different SAT participation policies, their average SAT scores are not directly comparable without adjustment.  
This project shows that participation structure explains a large part of score differences, and machine learning models perform best when this structure is explicitly modeled.

---

## Author
Rohit K. Bhatnagar