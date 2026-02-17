## **Summary**

For my CapStone project I seek to determine whether a U.S. state's average SAT performance can be accurately predicted using publicly available demographic, socioeconomic, and educational indicators. The goal is to understand which state‑level factors such as income, participation rates, school funding, and population characteristics—most strongly influence SAT outcomes and how these factors interact to shape college‑readiness performance across states.

---

## **Problem Statement**
Educational outcomes across the United States vary significantly from state to state due to differences in socioeconomic conditions, demographic composition, and the resources available within each state’s education system. While the College Board publishes annual SAT Suite of Assessments reports for each state, these reports provide descriptive summaries rather than predictive insights.

This project investigates the following question:

**Can we predict a state’s average SAT performance using publicly available demographic, socioeconomic, and educational indicators?**

The goal is to build a regression model that estimates each state’s mean SAT Total score (and its ERW and Math components) using data from three major sources:

- College Board SAT Suite State Reports  
- National Center for Education Statistics (NCES)  
- U.S. Census Bureau American Community Survey (ACS)

By integrating these datasets, the project aims to identify the factors most strongly associated with SAT performance and provide insights that can support educational planning and policy decisions.

---

## **Motivation & Benefits**

### **Why This Matters**
- SAT performance is a key indicator of college readiness.  
- States differ widely in income, demographics, and school resources.  
- Understanding these relationships can guide targeted interventions.

### **Benefits**
- Helps policymakers identify structural inequities.  
- Supports resource allocation decisions.  
- Demonstrates how multi‑source public datasets can be integrated for predictive modeling.  
- Provides a scalable framework for future educational analytics.

---

## **Data Needed**

For data needed for this project, we will require state‑level data from multiple public sources, including:

- **SAT participation and performance metrics** (e.g., mean ERW, Math, Total scores; benchmark attainment; demographic distributions)  
- **Socioeconomic indicators** (e.g., median household income, poverty rate, educational attainment, racial composition)  
- **Education system characteristics** (e.g., per‑pupil spending, student–teacher ratios, graduation rates, enrollment)

These data will be sourced from:
### **A. College Board SAT Suite Annual State Reports**
**Purpose:**  
- SAT participation  
- Mean ERW, Math, Total scores  
- Demographic distributions  
- Income quintile performance  
- Benchmark attainment  

**Citation:**  
College Board. *SAT Suite of Assessments Annual Reports.*  
[https://satsuite.collegeboard.org/media/pdf](https://satsuite.collegeboard.org/media/pdf)

---

### **B. NCES (National Center for Education Statistics)**
**Purpose:**  
- State‑level school characteristics  
- Teacher‑student ratios  
- Per‑pupil expenditures  
- Graduation rates  

**Citation:**  
NCES Education Data Explorer  
[https://nces.ed.gov/ccd/elsi/](https://nces.ed.gov/ccd/elsi/)

---

### **C. U.S. Census Bureau — American Community Survey (ACS)**
**Purpose:**  
- Median household income  
- Poverty rates  
- Racial/ethnic composition  
- Urban/rural distribution  
- Educational attainment  

**Citation:**  
U.S. Census Bureau — ACS  
`https://www.census.gov/programs-surveys/acs` [(census.gov in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fwww.census.gov%2Fprograms-surveys%2Facs")

---

## **Techniques to Be Used**

To model SAT performance and identify the strongest predictors, we plan to use supervised machine learning techniques such as:

- **Linear Regression**  
- **Ridge Regression**  
- **Random Forest Regression**

These methods will allow us to predict continuous SAT score outcomes and evaluate the relative importance of each feature.

---