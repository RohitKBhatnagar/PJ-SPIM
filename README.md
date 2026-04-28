# PJ-SPIM
PrepJolt - SAT Performance Intelligence Model (PJ-SPIM) :: Predicting State‑Level SAT Performance Using Multi‑Source Educational Data.

# Predicting U.S. SAT Performance via Socioeconomic & Educational Indicators

## Project Summary
This Capstone project investigates whether a U.S. state's average SAT performance can be accurately predicted using publicly available demographic, socioeconomic, and educational indicators. By integrating datasets from the **College Board**, **NCES**, and the **U.S. Census Bureau**, we built a predictive framework to identify the structural factors most strongly associated with college readiness.

## Key Findings
* **Predictive Anchors**: Educational attainment (`pct_bachelors_higher`) and Participation Rates emerged as the most significant predictors across both Random Forest and XGBoost models.
* **Model Performance**: Our baseline Random Forest model achieved an $R^2$ of 0.1454, indicating that while state-level socioeconomic factors are influential, they account for approximately 14.5% of the total variance in SAT scores.
* **Non-Linear Dynamics**: Partial Dependence Plots revealed a "participation cliff," where scores drop sharply as testing moves from self-selected elite groups to a general student population.

## Repository Structure
* `Capstone_SAT_Analysis.ipynb`: Main Jupyter Notebook containing EDA, Cleaning, and Modeling.
* `data/`: Directory containing raw and processed CSV files from Census, NCES, and College Board.
* `plots/`: Visualizations including Feature Importance and Residual Plots.

## Requirements
* Python 3.x
* Pandas, NumPy, Scikit-Learn, XGBoost, Matplotlib, Seaborn
