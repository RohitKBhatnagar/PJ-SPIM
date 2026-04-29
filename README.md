# **SAT Performance and Socioeconomic Determinants: A Multi‑Year State‑Level Analysis (2019–2024)**

**Author:** *Rohit K. Bhatnagar*

---

## **Executive Summary**

This project investigates whether U.S. state‑level SAT performance can be predicted using publicly available socioeconomic, demographic, and educational indicators. By integrating multi‑year data from the College Board, U.S. Census ACS, and NCES, the analysis evaluates how income, poverty, educational attainment, and participation policies shape observed SAT outcomes. Using both linear and nonlinear modeling approaches, the project demonstrates that participation rate is the dominant structural driver of state‑level SAT scores, while socioeconomic factors exert secondary but meaningful influence. The findings highlight the importance of contextualizing SAT results within broader demographic and policy environments rather than interpreting them as direct measures of academic quality.

---

## **Rationale**

State‑level SAT scores are widely referenced in discussions of educational quality, college readiness, and policy effectiveness. However, raw SAT averages are deeply shaped by socioeconomic conditions and participation policies that vary dramatically across states. Without adjusting for these structural factors, comparisons between states can be misleading and may reinforce inaccurate narratives about school system performance. This project addresses the need for a more rigorous, data‑driven understanding of the determinants of SAT outcomes and provides a reproducible framework for educational analytics using public data.

---

## **Research Question**

**Can a state’s average SAT performance be accurately predicted using publicly available demographic, socioeconomic, and educational indicators?**

Sub‑questions include:

- How strongly do income, poverty, and educational attainment correlate with SAT scores?  
- How does participation rate influence observed performance?  
- Which states over‑ or under‑perform relative to their socioeconomic context?  
- Are these relationships stable across multiple years (2019–2024)?  

---

## **Data Sources**

This project integrates data from three major public sources:

### **1. College Board — SAT Suite of Assessments State Reports**
- Participation rates  
- Mean ERW, Math, and Total scores  
- Demographic distributions  
- Benchmark attainment  

Official SAT State Reports (PDFs and data summaries):  
🔗 [https://satsuite.collegeboard.org/sat/data](https://satsuite.collegeboard.org/sat/data)  

### **2. U.S. Census Bureau — American Community Survey (ACS)**
- Median household income (DP03)  
- Poverty rate (DP03)  
- Educational attainment (DP02)  

ACS Program Overview:  
🔗 `https://www.census.gov/programs-surveys/acs` [(census.gov in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fwww.census.gov%2Fprograms-surveys%2Facs")  

ACS Data Access Portal (DP02, DP03 tables):  
🔗 [https://data.census.gov](https://data.census.gov) 

### **3. National Center for Education Statistics (NCES)**
- State‑level school characteristics  
- Per‑pupil expenditures  
- Student‑teacher ratios  
- Graduation rates  

NCES Main Site:  
🔗 [https://nces.ed.gov](https://nces.ed.gov)  

NCES Education Data Explorer:  
🔗 [https://nces.ed.gov/ccd/elsi](https://nces.ed.gov/ccd/elsi)

All datasets were cleaned, standardized, and merged into a multi‑year panel for analysis.

---

## **Methodology**

The project follows a structured analytical workflow:

1. **Data Engineering & Integration**  
   - Parsing and cleaning ACS DP02/DP03 files  
   - Standardizing College Board SAT data  
   - Merging multi‑year datasets into a unified panel  

2. **Exploratory Data Analysis (EDA)**  
   - Distributional analysis of SAT scores  
   - Scatterplots for income, education, and participation  
   - Correlation matrix and outlier identification  

3. **Feature Engineering**  
   - Participation normalization  
   - Multicollinearity assessment using VIF  
   - Construction of modeling dataset  

4. **Modeling**  
   - Baseline Linear Regression  
   - Random Forest Regression  
   - Performance comparison (RMSE, MAE, R²)  
   - Feature importance analysis  

5. **Interpretation & Policy Analysis**  
   - Socioeconomic gradients  
   - Participation‑driven structural effects  
   - Identification of anomalous states  

---

## **Results**

Key findings include:

- **Participation rate is the dominant predictor** of SAT scores, with a strong negative correlation (≈ –0.85).  
- **Income and educational attainment are positively associated** with SAT performance but are highly collinear.  
- **Poverty rate negatively influences SAT scores**, though its effect is smaller than participation.  
- **Random Forest models outperform linear regression**, indicating nonlinear interactions among predictors.  
- **Outlier states** such as the District of Columbia (high income, low scores) and Mississippi (low income, high scores) illustrate how participation policies distort raw averages.  
- Relationships remain **stable across 2019–2024**, reinforcing the robustness of the findings.

---

## **Next Steps**

Future work may include:

- Incorporating NCES funding, staffing, and resource variables  
- Developing hierarchical or multilevel models to capture nested structures  
- Constructing a composite socioeconomic index to reduce multicollinearity  
- Building an interactive dashboard for ongoing monitoring  
- Extending the analysis to ACT‑dominant states or district‑level data  

---

## **Outline of Project**

[Capstone SAT Notebook](https://github.com/RohitKBhatnagar/PJ-SPIM/blob/main/CapStone_SAT.ipynb)

### **📘 Key Components and Results from the Capstone Jupyter Notebook**

This section provides a structured overview of the analytical workflow, data engineering steps, exploratory analysis, and modeling results contained in the Jupyter notebook *CapStone_SAT-Final.ipynb*. It is designed for readers of the GitHub repository who need a concise but comprehensive understanding of the project.

---

#### **1. Data Understanding & Preparation**

##### **1.1 Environment Setup**
The notebook initializes a reproducible environment using:
- `pandas`, `numpy` for data manipulation  
- `matplotlib`, `seaborn` for visualization  
- `glob`, `os`, `re` for file handling  
- Custom helper functions for Census and SAT cleaning  

All visualizations use a consistent professional theme (`seaborn-v0_8-muted` + `viridis` palette).

---

##### **1.2 Census Data Processing (ACS DP02 & DP03)**

The notebook implements robust cleaning functions to handle:
- Double‑header ACS CSV files  
- Year extraction from filenames  
- Standardization of state names  
- Extraction of key socioeconomic indicators:
  - **Median household income (DP03_0062E)**
  - **Poverty rate (DP03_0128PE)**
  - **Educational attainment: % Bachelor’s+ (DP02_0068PE)**

**Result:**  
Successfully processed **5 years (2019, 2021–2024)** with **260 state‑year records**.

---

##### **1.3 SAT Data Processing (College Board)**

The notebook:
- Loads 6 years of SAT State Reports  
- Standardizes column names  
- Extracts participation rate, mean scores, and demographic fields  
- Selects **`sat_50th_total`** as the modeling target  

**Result:**  
SAT master dataset: **318 records**, 248 variables.

---

##### **1.4 Merging SAT + Census Data**

A full inner join on `state` and `year` produces:

- **260 merged records** (expected ≈ 250)  
- No missing values in key socioeconomic fields  
- Final cleaned modeling dataset: **255 records**, 251 variables  

---

#### **2. Exploratory Data Analysis (EDA)**

##### **2.1 SAT Score Distributions (2019–2024)**  
Findings:
- Unimodal distributions across all years  
- Stable central tendency  
- Mild right‑skewness (high‑performing outliers)  
- Year‑to‑year shifts likely driven by participation policies and pandemic effects  

---

##### **2.2 Participation Rate vs SAT Scores**

A clear **strong negative relationship**:
- Low‑participation states → inflated SAT scores  
- High‑participation states → population‑level scores  
- Participation rate is a **structural confounder**, not a causal factor  

---

##### **2.3 Income vs SAT Performance**

Key insights:
- Strong positive association between income and SAT scores  
- Educational attainment amplifies this gradient  
- High‑income states cluster tightly; low‑income states show wider variability  
- Outliers reflect participation policies and demographic differences  

---

##### **2.4 Correlation Matrix**

Major relationships:
- **Participation rate ↘ SAT scores (–0.85)**  
- **Income ↗ Education (0.81)**  
- **Income ↗ SAT scores (0.33)**  
- **Poverty ↘ SAT scores (–0.07)**  

Participation rate is the **dominant linear correlate**.

---

#### **3. Feature Engineering**

##### **3.1 Participation Normalization**
Converted participation to a 0–1 ratio.  
Identified **98 high‑participation state‑years** (>50%), which consistently show lower SAT scores due to universal testing.

---

##### **3.2 Multicollinearity (VIF Analysis)**

| Feature | VIF |
|--------|------|
| pct_bachelors_higher | **85.47** |
| median_income | **77.33** |
| poverty_rate | 8.97 |
| part_ratio | 2.69 |

Interpretation:
- Income and educational attainment are **highly collinear**  
- Participation rate is independent and structurally dominant  

---

#### **4. Modeling**

##### **4.1 Baseline Linear Regression**

**Performance:**
- RMSE: **73.87**  
- MAE: **44.90**  
- R²: **0.593**

**Coefficient interpretation:**
- `part_ratio`: **–285** (largest effect; universal testing lowers scores)  
- `poverty_rate`: **–17.7** (higher poverty → lower scores)  
- `pct_bachelors_higher`: **+2.9** (small positive effect)  
- `median_income`: **–0.0025** (sign flip due to multicollinearity)

Linear regression captures broad trends but struggles with nonlinearities.

---

##### **4.2 Random Forest Regression**

**Performance:**
- RMSE: **59.36**  
- MAE: **29.09**  
- R²: **0.737**

**Feature Importance:**
- `part_ratio`: **~0.85** (dominant predictor)  
- `poverty_rate`: moderate importance  
- `median_income`, `pct_bachelors_higher`: minimal unique contribution  

Random Forest outperforms linear regression, confirming **nonlinear interactions** and **threshold effects**.

---

#### **5. Key Insights & Conclusions**

- Participation rate is the **primary driver** of observed SAT scores.  
- Income and educational attainment form a **shared socioeconomic gradient**.  
- Poverty exerts a meaningful but secondary influence.  
- Outlier states (e.g., DC, Mississippi) reflect participation structures, not academic anomalies.  
- Relationships remain **stable across 2019–2024**, reinforcing robustness.  
- Policy interpretation must account for **testing mandates** and **demographic context**.

---

## **Contact and Further Information**

For questions, collaboration, or further discussion, please contact:

**Rohit K. Bhatnagar**  