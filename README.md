# Women in Parliament and Health Expenditures

**An econometric analysis of female political representation and government health spending across 161 countries (2000–2018)**

Final Paper — Econometrics, Fall Semester 2025

---

## Overview

This project investigates whether greater representation of women in national parliaments is associated with higher government health expenditures, and whether this relationship depends on a country's level of economic development.

Using panel data from the World Bank covering **161 countries** over **2000–2018** (2,868 observations), we estimate two-way fixed effects models with an interaction between female parliamentary representation and (log) GDP per capita.

### Key Findings

- **No unconditional effect:** Once country and year fixed effects are included, the positive association between women's parliamentary representation and health spending becomes statistically insignificant.
- **Conditional effect:** There is weak evidence (significant at the 10% level) that the relationship is moderated by economic development. For countries with GDP per capita above roughly **$18,000**, higher female representation is associated with a positive and significant increase in health spending.
- **Magnitude:** At higher income levels (~$45,000 GDP per capita), a 10-percentage-point increase in women's parliamentary representation is associated with roughly a **0.6 percentage-point** increase in the share of health spending.
- **Lagged specification:** When independent variables are lagged, the interaction becomes significant at the **95% level** for high-income countries, strengthening the conditional finding.

---

## Research Hypotheses

| # | Hypothesis |
|---|-----------|
| **H1** | Greater representation of women in national parliaments is associated with a higher proportion of health-related spending. |
| **H2** | The positive association between women's representation and health-related spending is stronger in countries with higher levels of economic development. |

---

## Data

| Source | World Bank |
|--------|-----------|
| **Coverage** | 161 countries, 2000–2018 |
| **Observations** | 2,868 (unbalanced panel) |

### Variables

**Dependent variable**
- `health_exp` — Domestic general government health expenditure (% of general government expenditure)

**Key independent variables**
- `women_prob` — Proportion of seats held by women in national parliaments (%)
- `log_gdp_pcap` — Log of GDP per capita (moderator)

**Controls**
- `democ_index` — Democracy Index (political regime)
- `urban_pop` — Urban population (% of total)
- `labour_fem` — Female labor force participation (%)
- `life_exp` — Life expectancy at birth (years)

---

## Repository Structure

```
.
├── README.md
├── report.pdf                  # Final paper
├── 2301_Semenova_slides.pdf    # Presentation slides
├── report.qmd                  # Quarto source file (full analysis)
├── bibiography.bib             # Literature included
└── data/                       # Folder with .csv file with data
```

---

## Methodology

- **Model:** Ordinary Least Squares with two-way fixed effects (country + year)
- **Interaction model:**

  ```
  HealthExp_it = β₁·WomenParl_it + β₂·LogGDPpc_it
               + β₃·(WomenParl_it × LogGDPpc_it)
               + θ_i + δ_t + ε_it
  ```

- **Standard errors:**
  - Pooled OLS → heteroskedasticity-robust
  - Panel specifications → clustered at the country level
- **Robustness:** Lagged independent variables (Table 6, Figure 5)

---

## Replication

### Requirements

- **R** (≥ 4.3) with the following packages:
  `tidyverse`, `fixest`, `modelsummary`, `xtsum`, `plm`, `marginaleffects`, `sjPlot`, `interactions`, `scales`, `showtext`, `extrafont`, `viridis`, `kableExtra`, `corrplot`
- **Quarto** (to render the `.qmd` file)

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```

2. Place the raw World Bank data in `data/raw/`.

3. Render the analysis:
   ```bash
   quarto render analysis.qmd
   ```

---

## Results Summary

| Model | Specification | Coefficient on Women in Parliament |
|-------|--------------|-----------------------------------|
| (1) | Pooled OLS | 0.135*** |
| (2) | + Controls | 0.058** |
| (3) | + Country FE | 0.027* |
| (4) | + Year FE | 0.070*** |
| (5) | Two-way FE | 0.007 (n.s.) |
| (6) | + Interaction | −0.146* |

*Significance: \*p<0.1, \*\*p<0.05, \*\*\*p<0.01*

The marginal effect plot (Figure 4) shows that the effect of female representation turns positive and significant (90% CI) once GDP per capita exceeds ~$18,000.

---

## Limitations

- **Omitted political factors** — government ideology, party composition, and gender quotas are not accounted for.
- **Reverse causality** — social welfare policies may themselves influence women's political participation.
- **Measurement** — seat shares do not capture substantive influence (committee roles, party cohesion).
- **Western bias** — theoretical mechanisms largely derived from OECD contexts.
- **Expenditure shares** — cannot distinguish absolute spending changes from reallocation.

---

## Authors & Contributions

| Name | Contributions |
|------|--------------|
| **Altysheva Zhanna** | Conceptualization, literature review, research design, data collection & preprocessing, regression analysis, results, project management |
| **Emshanova Evgeniia** | Conceptualization, research design, introduction, data & measurement |
| **Obukhova Ekaterina** | Conceptualization, literature review, research design, data preprocessing, visualization, discussion & limitations |
| **Semenova Kseniia** *(Team Leader)* | Conceptualization, literature review, research design, regression analysis, statistical model, results, conclusion, full draft revision, project management |
| **Fradkina Tatiana** | Conceptualization, research design, data preprocessing, visualization, data & measurement |

---

## Declaration of AI Use

The report was developed using Claude 4.5 Sonnet (Anthropic) to obtain feedback on text clarity, flow, and coherence.

---

## References

Key sources include Anwar et al. (2023), Clayton & Zetterberg (2018), Clots-Figueras (2011), Cinelli et al. (2024), Hessami & Fonseca (2020), Mavisakalyan (2012), and Wängnerud (2009). See `report.pdf` for the full reference list.
