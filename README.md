# Day 3 vs Day 5 Embryo Transfer: IVF Outcomes Analysis

Comparative analysis of cleavage-stage (Day 3) versus blastocyst-stage (Day 5) embryo transfers using a clinical IVF dataset. All analyses were performed in R.

---

## Data

The dataset contains **222 IVF cycles** from **177 unique patients**, with some patients contributing multiple cycles. Data are stored in two sheets:

- **`cycles`** — one row per cycle; includes patient demographics (age, BMI, gravidity, sperm origin), laboratory metrics (oocyte counts, fertilization, embryo development), and clinical outcomes (implantation, pregnancy, live birth)
- **`Oocyte-level embryo development`** — one row per oocyte; includes maturation stage at retrieval, fertilization status, and Day 5 blastocyst grading

> Raw data files are not included in this repository.

---

## Outcomes

**Laboratory**
- Oocytes retrieved, MII oocytes, MII rate (%)
- Fertilized oocytes (2PN), fertilization rate (%)
- Embryos at Day 3, cleavage rate (%)
- Embryos transferred
- Blastocysts at Day 5, blastulation rate (%) — *Day 5 cycles only*

**Clinical**
- Implantation (≥1 gestational sac)
- Implantation rate (sacs / embryos transferred)
- Clinical pregnancy
- Live birth (> 24 weeks)

---

## Statistical Methods

| Variable | Unit | Test |
|---|---|---|
| Age, BMI | Patient | Wilcoxon rank-sum |
| Age group, BMI group, sperm origin | Patient | Chi-squared |
| Continuous cycle outcomes | Cycle | GEE — Gaussian |
| Binary outcomes | Cycle | GEE — Binomial logit |
| Implantation rate | Cycle | GEE — Gaussian |

- **GEE** (Generalised Estimating Equations) models use an exchangeable correlation structure clustered by patient to account for repeated cycles
- Significance assessed via **GEE Wald test** (χ², 1 df)
- Descriptive statistics reported as **mean ± SEM** and **median [IQR]**
- Rates expressed as percentages; implantation rate capped at 100%
- Blastocyst outcomes reported descriptively for Day 5 cycles only (no Day 3 comparison)

---

## Required Packages

```r
install.packages(c(
  "readxl",      # read Excel data files
  "tidyverse",   # data wrangling and visualisation
  "scales",      # axis label formatting
  "patchwork",   # combine ggplot panels
  "ggridges",    # ridge and raincloud plots
  "geepack",     # GEE models
  "emmeans",     # marginal means from GEE models
  "gtsummary",   # summary tables
  "gt",          # table rendering
  "openxlsx",    # Excel export
  "knitr",       # R Markdown
  "kableExtra",  # table formatting
  "networkD3",   # Sankey diagrams
  "htmltools"    # HTML widget layout
))
```

---

## Output

Running the `.Rmd` file produces an HTML report containing:

- Patient demographics table (Table 1)
- Fertility and cycle outcomes table with GEE p-values (Table 2)
- GEE results table: mean ± SE by group (Table 3)
- Figures: age/BMI distributions, GEE bar plots, binary outcome plots, Sankey flow diagram (embryos → sacs → live births)
- Summary tables for all plots
- Excel export of all tables and raw data (`IVF_Analysis_Output/All_Tables.xlsx`)

---

## Repository Structure

```
.
├── IVF_Analysis_Report.Rmd   # main analysis script
├── sampled_patients177.csv   # patient ID list
└── README.md
```
