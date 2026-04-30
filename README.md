<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:581C87,50:7E22CE,100:9333EA&height=220&section=header&text=NYC+Housing+Equity+Analysis&fontSize=48&fontColor=fff&animation=twinkling&fontAlignY=38&desc=Who+Is+Being+Displaced+from+New+York+City+%E2%80%94+and+Why%3F&descAlignY=62&descSize=18" />

<br/>

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&pause=1000&color=A855F7&center=true&vCenter=true&width=750&lines=R+%2B+randomForest+%2B+Census%2FACS+Population+Data;Displacement+Risk+Modeling+Across+NYC+Boroughs;Reproducible+Quarto+Report+%2B+Full+Methodology+Docs;Data+Analysis+in+Service+of+Housing+Equity)](https://github.com/yashxsainix/STA9750-2025-FALL)

<br/>

[![R](https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white)](https://www.r-project.org)
[![Quarto](https://img.shields.io/badge/Quarto-Reproducible_Report-9333EA?style=for-the-badge)](https://quarto.org)
[![randomForest](https://img.shields.io/badge/randomForest-Statistical_Modeling-7E22CE?style=for-the-badge)](https://cran.r-project.org/web/packages/randomForest)
[![Census ACS](https://img.shields.io/badge/Data-Census_%2F_ACS-581C87?style=for-the-badge)](https://www.census.gov/programs-surveys/acs)

<br/>

<img src="https://img.shields.io/badge/Boroughs_Analyzed-5_NYC-581C87?style=flat-square&labelColor=0D1117" />
<img src="https://img.shields.io/badge/Data_Source-Census_%2B_ACS-7E22CE?style=flat-square&labelColor=0D1117" />
<img src="https://img.shields.io/badge/Model-randomForest_%2B_Regression-9333EA?style=flat-square&labelColor=0D1117" />
<img src="https://img.shields.io/badge/Output-Reproducible_Quarto_Report-A855F7?style=flat-square&labelColor=0D1117" />

</div>

---

## 🏙️ The Question

New York City has been changing for decades. Neighborhoods gentrify. Longtime residents move out. Communities that built a borough over generations find themselves displaced by rising rents and shifting economic pressures.

This project asks: **which NYC neighborhoods are at the highest risk of displacement, and what demographic and economic factors predict that risk?**

The answer matters for policy, for housing advocacy, and for anyone trying to understand how the city is changing.

---

## 🔬 Methodology

```mermaid
graph TD
    A["📊 Data Collection\nCensus ACS 5-Year Estimates\nAmerican Community Survey\nNYC borough-level data"] --> B["🔧 Data Preparation\n• Feature engineering\n• Null handling\n• Variable standardization\n• Train/test split"]

    B --> C["📐 Statistical Modeling"]

    C --> D["📈 OLS Regression\nLinear displacement\nrisk factors\nCoefficient interpretation"]

    C --> E["🌲 randomForest\nNon-linear risk modeling\nFeature importance ranking\nOut-of-bag error estimation"]

    D & E --> F["📋 Reproducible Report\nQuarto document\nAll methodology documented\nFindings + recommendations\nfor policy audiences"]

    G["🗺️ Geographic Analysis\nBorough-level mapping\nNeighborhood comparison\nSpatial risk distribution"] --> F

    style A fill:#581C87,color:#fff,stroke:#581C87
    style C fill:#7E22CE,color:#fff,stroke:#7E22CE
    style F fill:#9333EA,color:#fff,stroke:#9333EA
```

---

## 📊 Variables Analyzed

<details>
<summary><b>🏘️ Housing Indicators</b></summary>

- Median gross rent as a percentage of household income
- Renter-occupied housing unit percentage
- Housing unit vacancy rate
- Median home value
- Rent burden (>30% of income on housing)
- Severe rent burden (>50% of income on housing)

</details>

<details>
<summary><b>👥 Demographic Indicators</b></summary>

- Racial and ethnic composition by census tract
- Percentage of foreign-born residents
- Educational attainment distribution
- Median household income
- Poverty rate
- Population change over time

</details>

<details>
<summary><b>📈 Economic Indicators</b></summary>

- Unemployment rate
- Median household income trend
- Income inequality (Gini coefficient)
- Industry employment distribution
- Commute time (proxy for accessibility)

</details>

---

## 🌲 Why randomForest

OLS regression gives interpretable coefficients — useful for policy communication. But displacement risk is not necessarily linear. Neighborhoods with moderate values across several risk factors may be at higher actual risk than neighborhoods with one extreme indicator.

randomForest captures these interaction effects without requiring you to specify them explicitly. The model's **variable importance output** then tells you which factors contributed most to predictive accuracy — giving you the non-linear insight alongside the interpretable regression results.

```r
# Model training
library(randomForest)

rf_model <- randomForest(
  displacement_risk ~ median_rent_burden + pct_renters + 
                      income_change + pct_poc + vacancy_rate,
  data = train_data,
  ntree = 500,
  importance = TRUE
)

# Variable importance
varImpPlot(rf_model)
```

---

## 📋 The Reproducible Report

Every finding in this analysis is reproducible. The Quarto document includes:

- All data sources with links and access dates
- Full data cleaning and transformation code
- Model specifications and parameter choices
- Diagnostic plots and residual analysis
- Interpretation guidance for policy audiences
- Limitations section with clear caveats

The goal is that another researcher could take this document, run it on updated ACS data, and produce a current analysis without guessing what was done or why.

---

## 🗂️ Repository Structure

```
STA9750-2025-FALL/
│
├── analysis/
│   ├── housing_equity_analysis.qmd    ← Main Quarto document
│   └── housing_equity_analysis.html   ← Rendered report
│
├── data/
│   ├── raw/                           ← ACS/Census downloads
│   └── processed/                     ← Cleaned analysis-ready data
│
├── R/
│   ├── data_prep.R                    ← Cleaning functions
│   ├── modeling.R                     ← Regression + randomForest
│   └── visualization.R               ← Charts and maps
│
└── outputs/
    ├── figures/                       ← All plots
    └── tables/                        ← Summary statistics
```

---

## 🚀 How to Run

```r
# Install required packages
install.packages(c("tidyverse", "randomForest", "tidycensus", "quarto"))

# Set Census API key
tidycensus::census_api_key("YOUR_KEY_HERE", install = TRUE)

# Render the full analysis
quarto::quarto_render("analysis/housing_equity_analysis.qmd")
```

---

## 💡 Why This Matters

Data analysis in service of equity is one of the most valuable applications of statistical methodology. This project demonstrates that the same tools used for financial modeling and business analytics can be turned toward understanding how communities change and how policy decisions affect real people.

The technical skills are identical. The stakes are different.

---

## 👤 Author

**Yashpal Saini** · [LinkedIn](https://linkedin.com/in/yash-saini-analyst) · [Portfolio](https://yashxsainix.github.io)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:581C87,50:7E22CE,100:9333EA&height=100&section=footer" />
