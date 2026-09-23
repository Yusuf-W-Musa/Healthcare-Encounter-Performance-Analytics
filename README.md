# 🏥 Healthcare Encounter Performance Analytics

> **An end-to-end healthcare business intelligence, predictive analytics, and prescriptive analytics project using Power BI, Power Query, DAX, statistical modelling, forecasting, and What-If analysis to evaluate patient encounters, readmissions, operational performance, and financial outcomes.**

---

## Project Overview

Healthcare organizations generate large volumes of data across patient encounters, providers, facilities, diagnoses, procedures, payers, costs, and treatment activity. The challenge is not simply storing this information, but transforming it into reliable insights that support operational and managerial decision-making.

This project develops a comprehensive **Healthcare Encounter Performance Analytics solution** using Microsoft Power BI.

The analysis integrates eight healthcare tables into a structured analytical model and examines performance across four major areas:

* patient and encounter activity;
* clinical and readmission patterns;
* provider and facility performance;
* financial and payer performance.

The project was subsequently extended beyond descriptive reporting to include:

* diagnostic analytics;
* external inflation benchmarking;
* multiple linear regression;
* six-month revenue forecasting;
* Power BI Key Influencers analysis;
* cost-reduction What-If modelling;
* length-of-stay optimization scenarios; and
* management-oriented recommendations.

The final solution therefore moves through the full analytical progression:

```text
Descriptive Analytics
        ↓
Diagnostic Analytics
        ↓
Predictive Analytics
        ↓
Prescriptive Analytics
```

Rather than simply reporting what happened, the project investigates **why performance differs, what future performance may look like, and how operational changes could affect financial and capacity outcomes.**

---

# Business Problem

Healthcare managers need to understand how patient activity, clinical outcomes, operational performance, and financial results interact.

A traditional report may answer questions such as:

> How many encounters occurred?

A more useful analytical system should also answer:

> Which patient, facility, procedure, diagnosis, and payer combinations are associated with elevated readmission?

> Where are operational differences occurring?

> Are charges and costs moving together?

> How is financial performance changing over time?

> What could future revenue look like?

> What happens to cost and capacity if operational efficiency improves?

This project was designed to address these questions using an integrated Power BI analytics framework.

---

# Project Objectives

The project focuses on six major analytical objectives.

### 1. Build a reliable healthcare analytical model

Transform multiple healthcare source tables into a clean, relationship-driven Power BI model suitable for analytical reporting.

### 2. Measure encounter and patient performance

Evaluate encounter volume, patient activity, length of stay, readmissions, diagnoses, procedures, and utilization patterns.

### 3. Compare provider and facility performance

Identify meaningful variation across healthcare providers and facilities while avoiding conclusions based on very small sample sizes.

### 4. Evaluate financial performance

Analyze charges, cost, margin, payer mix, and financial trends.

### 5. Develop predictive insight

Use forecasting and multiple linear regression to estimate future financial performance and understand relationships between revenue, cost, and encounter volume.

### 6. Support prescriptive decision-making

Use Power BI What-If parameters to estimate the potential financial and operational impact of cost reduction and length-of-stay improvement scenarios.

---

# Analytical Framework

The project progresses through four levels of analytics.

| Analytics Type   | Main Question         | Project Application                                            |
| ---------------- | --------------------- | -------------------------------------------------------------- |
| **Descriptive**  | What happened?        | Encounters, patients, LOS, readmissions, charges, cost, margin |
| **Diagnostic**   | Why did it happen?    | Procedure, payer, facility and readmission investigations      |
| **Predictive**   | What may happen next? | Revenue forecasting and regression                             |
| **Prescriptive** | What could we do?     | Cost and LOS What-If scenarios                                 |

This progression makes the dashboard more useful for decision support than a purely descriptive reporting solution.

---

# Dataset Overview

The core analytical dataset contains:

| Metric                     |         Value |
| -------------------------- | ------------: |
| Healthcare Encounters      |     **1,500** |
| Distinct Patients          |       **479** |
| Providers                  |       **100** |
| Facilities                 |        **10** |
| Encounter Period           | **2019–2021** |
| Monthly Analytical Periods |        **36** |
| Total Readmissions         |       **229** |
| Overall Readmission Rate   |    **15.27%** |

The source data are organized across eight healthcare tables representing encounters and related dimensions.

---

# Data Model

The Power BI model follows a **star-schema design**.

The central encounter fact table is surrounded by descriptive dimension tables.

```text
                     ┌──────────────────┐
                     │  Calendar Table  │
                     └────────┬─────────┘
                              │
                              │
┌────────────────┐            │             ┌────────────────┐
│ Patient Table  │────────────┼─────────────│ Provider Table │
└────────────────┘            │             └────────────────┘
                              │
                     ┌────────▼─────────┐
                     │ Encounter Table  │
                     │   Fact Table     │
                     └────────┬─────────┘
                              │
       ┌──────────────────────┼───────────────────────┐
       │                      │                       │
       ▼                      ▼                       ▼
┌──────────────┐      ┌───────────────┐      ┌──────────────┐
│Facility Table│      │Diagnosis Table│      │Procedure Table│
└──────────────┘      └───────────────┘      └──────────────┘
                              │
                              ▼
                      ┌─────────────┐
                      │ Payer Table │
                      └─────────────┘
```

An additional disconnected **Medical Care CPI** table is used for external financial benchmarking.

---

# Why a Star Schema?

A star schema was selected because it provides:

* clear separation between transactional and descriptive data;
* simpler relationships;
* efficient filtering;
* easier DAX development;
* reduced ambiguity;
* improved Power BI performance; and
* a scalable foundation for additional analytical measures.

The model primarily uses single-direction **one-to-many relationships** between the dimension tables and the Encounter fact table.

---

# Data Preparation & ETL

Power Query was used to clean, validate, transform, and prepare the source data before modelling.

The workflow included:

```text
Raw Healthcare Tables
        ↓
Data Profiling
        ↓
Type Validation
        ↓
Missing / Invalid Value Review
        ↓
Discharge-Date Correction
        ↓
Derived Attributes
        ↓
Calendar Construction
        ↓
Relationship Validation
        ↓
Star Schema
        ↓
DAX Measures
        ↓
Dashboard & Analytics
```

---

## Discharge-Date Data Quality Issue

One of the most important data-quality problems involved invalid discharge-date relationships.

A total of:

```text
398 discharge date keys
```

required correction.

For affected records, discharge dates were reconstructed using:

```text
Corrected Discharge Date
=
Admission Date + Length of Stay
```

The remaining:

```text
1,102 encounters
```

did not require the same correction.

This ensured that discharge timing was internally consistent with the reported length of stay.

---

# Calendar Table

A dedicated Calendar dimension was created to support time intelligence and consistent date filtering.

The calendar contains:

```text
1,461 dates
```

and extends through:

```text
December 31, 2022
```

Although encounter admissions primarily cover 2019–2021, the calendar was extended because corrected discharge activity reaches into 2022.

Additional date attributes support analysis by:

* year;
* quarter;
* month;
* month name;
* month number;
* year-month;
* start of month;
* start of quarter;
* start of year; and
* week.

---

# Additional Transformations

Several business-friendly analytical fields were created.

### Patient Profile

Patient characteristics were combined into a consolidated profile field for demographic analysis.

### Readmission Category

Encounter-level readmission status was transformed into interpretable categories for reporting and filtering.

### Time Intelligence Fields

Calendar attributes were created to support trends, year-over-year comparisons, forecasting, and CPI alignment.

---

# Core DAX Measures

The Power BI model contains a centralized collection of DAX measures covering healthcare utilization, clinical performance, and financial outcomes.

Major measures include:

### Encounter Measures

```text
Total Encounters
Distinct Patients
Encounters per Patient
Total Providers
Total Facilities
```

### Length-of-Stay Measures

```text
Total Inpatient Days
Average Length of Stay
```

### Readmission Measures

```text
Readmission Count
Readmission Rate
Readmission Rate by Procedure
Readmission Rate by Facility
Readmission Rate by Payer
```

### Financial Measures

```text
Total Charges
Total Cost
Gross Margin
Gross Margin %
Average Charge per Encounter
Average Cost per Encounter
```

The project uses approximately **26 DAX measures** across the analytical model.

---

# Baseline Healthcare Performance

The overall dashboard reports:

| KPI                    |        Result |
| ---------------------- | ------------: |
| Total Encounters       |     **1,500** |
| Distinct Patients      |       **479** |
| Total Readmissions     |       **229** |
| Readmission Rate       |    **15.27%** |
| Average Length of Stay | **7.62 days** |
| Total Inpatient Days   |    **11,434** |
| Total Charges          |   **$36.29M** |
| Total Cost             |   **$21.92M** |
| Gross Margin           |   **$14.38M** |
| Gross Margin %         |    **39.61%** |

These KPIs provide the baseline against which the more detailed diagnostic analysis is conducted.

---

# Dashboard Architecture

The Power BI report was designed as a multi-page analytical application rather than a single crowded dashboard.

The report includes:

```text
Home / Navigation
        │
        ├── Patient Overview
        │
        ├── Clinical & Diagnosis Insights
        │
        ├── Provider & Facility Performance
        │
        ├── Financial & Payer Analysis
        │
        └── Facility Detail Drill-Through
```

The design combines KPI monitoring with exploratory and diagnostic analysis.

---

# Page 1 — Patient Overview

The Patient Overview provides a high-level summary of healthcare utilization.

### Key metrics include:

* total encounters;
* distinct patients;
* average length of stay;
* total readmissions;
* readmission rate;
* encounter trends.

### Analytical questions include:

* How has encounter volume changed over time?
* What does the patient population look like?
* Which encounter categories are most common?
* Are utilization patterns stable across the analytical period?

Interactive slicers allow users to narrow the analysis by relevant dimensions.

---

# Page 2 — Clinical & Diagnosis Insights

The clinical page focuses on diagnosis, procedure, length of stay, and readmission behaviour.

A major diagnostic feature is the **Decomposition Tree**, which allows users to progressively investigate readmission patterns across dimensions such as:

```text
Readmission
    ↓
Procedure
    ↓
Payer
    ↓
Diagnosis
    ↓
Facility
```

This allows the user to move from a high-level anomaly toward increasingly specific combinations of patient-care characteristics.

---

# Page 3 — Provider & Facility Performance

This page compares operational performance across providers and healthcare facilities.

Measures include:

* encounter volume;
* readmission rate;
* length of stay;
* charges;
* costs;
* margin;
* procedure mix.

To reduce misleading comparisons caused by very small samples, a **minimum-volume threshold of 20 encounters** is incorporated into selected analyses.

A dedicated **Facility Detail drill-through page** allows users to move from high-level facility comparisons to a more detailed investigation.

---

# Page 4 — Financial & Payer Analysis

The financial page examines:

* charges;
* costs;
* gross margin;
* gross margin percentage;
* payer contributions;
* encounter-level financial performance; and
* financial change over time.

A **Waterfall Chart** is used to clearly communicate the relationship:

```text
Total Charges
      −
Total Cost
      =
Gross Margin
```

Overall:

```text
$36.29M Charges
− $21.92M Cost
────────────────
$14.38M Margin
```

with an overall gross margin of approximately:

```text
39.61%
```

---

# External Economic Benchmark — Medical Care CPI

An external benchmark was incorporated to strengthen interpretation of financial trends.

The project uses the U.S. Bureau of Labor Statistics:

> **Medical Care CPI-U — CUUR0000SAM**

The monthly CPI series is aligned with the healthcare model using a Year-Month key.

Because the CPI table is disconnected from the main star schema, DAX using `TREATAS` is used to apply the correct period context.

This enables comparison between:

```text
Healthcare Charge Growth
            vs.
Medical Care Price Inflation
```

and helps distinguish nominal financial changes from broader medical-price movements.

---

# Diagnostic Finding 1 — Imaging and Readmission

One of the strongest clinical findings involves imaging encounters.

### Imaging

```text
64 readmissions / 319 encounters
= 20.06%
```

### Non-Imaging

```text
13.97% readmission rate
```

The difference is approximately:

```text
6.09 percentage points
```

Imaging encounters therefore show a materially higher readmission rate within this dataset.

This does **not establish that imaging causes readmission**.

Instead, it identifies an area requiring deeper investigation into:

* diagnosis severity;
* patient condition;
* follow-up processes;
* repeat imaging;
* discharge planning; and
* care complexity.

---

# Diagnostic Finding 2 — Imaging + Private Payer

Further decomposition reveals a stronger pattern within the Imaging + Private payer combination.

The observed readmission rate is:

```text
25.86%
```

based on:

```text
15 readmissions / 58 encounters
```

The elevated pattern also appeared across both Acute and Chronic categories.

This indicates that the high imaging readmission rate is not evenly distributed across all payer groups.

### Recommended investigation

Healthcare management could review:

* discharge instructions;
* post-imaging follow-up;
* repeat imaging patterns;
* diagnosis mix;
* payer-specific care pathways;
* appointment scheduling; and
* readmission timing.

---

# Diagnostic Finding 3 — Facility Variation

Facility performance also differs materially.

### Facility 6

```text
166 encounters
30 readmissions
18.07% readmission rate
```

### Facility 4

```text
155 encounters
17 readmissions
10.97% readmission rate
```

Difference:

```text
7.10 percentage points
```

Facility 6 therefore warrants further investigation.

However, the dashboard intentionally avoids concluding that Facility 6 is necessarily delivering worse care.

Differences could result from:

* patient severity;
* procedure mix;
* diagnosis mix;
* payer composition;
* provider mix;
* referral patterns; or
* other unmeasured characteristics.

The correct next step is **risk-adjusted investigation**, not immediate causal attribution.

---

# Diagnostic Finding 4 — Charges vs Medical Inflation

From 2020 to 2021:

```text
Encounter Volume:     ↓ 8.24%
Total Charges:        ↓ 10.83%
Average Charge:       ↓ 2.82%
Medical Care CPI:     ↑ 1.23%
```

Therefore, average charge performance weakened even while medical-care prices increased.

The approximate inflation-adjusted gap is around:

```text
4 percentage points
```

This suggests that the decline in nominal performance may understate the economic pressure when healthcare inflation is considered.

Potential areas for review include:

* payer contracts;
* charge schedules;
* service mix;
* procedure volume;
* reimbursement arrangements; and
* cost containment.

---

# Payer Analysis

Payer analysis allows financial and clinical performance to be evaluated together.

For example, Medicare accounts for approximately:

```text
$8.20M in total charges
```

within the dataset.

Rather than evaluating payers only by financial contribution, the model also allows payer categories to be analyzed alongside:

* readmission;
* procedures;
* facility;
* diagnosis;
* cost;
* margin; and
* encounter volume.

This supports a more complete understanding of payer performance.

---

# Length of Stay and Cost

The analysis found a linear correlation of approximately:

```text
r ≈ -0.043
```

between length of stay and encounter cost.

This is effectively a negligible linear relationship within this dataset.

Therefore, it would be inappropriate to claim that longer stays automatically result in proportionally higher costs based on this analysis alone.

This demonstrates an important analytical principle:

> **A relationship that appears intuitively reasonable should still be tested rather than assumed.**

---

# Advanced Predictive Analytics

The project was extended beyond historical and diagnostic reporting to include predictive analytics.

Two major approaches were implemented:

1. **Multiple Linear Regression**
2. **Power BI Time-Series Forecasting**

---

# Multiple Linear Regression

A monthly regression model was developed to estimate total revenue.

Because actual collected revenue is not available in the dataset:

> **Total Charges are used as the analytical revenue proxy.**

This distinction is important because billed charges should not automatically be interpreted as realized cash revenue.

---

## Regression Target

```text
Monthly Total Revenue
```

where:

```text
Total Revenue = Total Charges
```

for analytical purposes.

---

## Predictors

The model uses:

```text
Total Cost
Encounter Count
```

as the explanatory variables.

The approximate estimated model is:

```text
Predicted Revenue
=
− $17,572
+ 1.363 × Total Cost
+ $4,806 × Encounter Count
```

---

# Regression Training Strategy

To preserve temporal order, the model was not evaluated using a purely random split.

### Training Period

```text
January 2019 – December 2020
24 months
```

### Testing Period

```text
January 2021 – December 2021
12 months
```

This creates a more realistic test in which earlier observations are used to estimate a later period.

---

# Regression Performance

Test-period performance was approximately:

| Metric   |      Result |
| -------- | ----------: |
| **R²**   |  **97.67%** |
| **MAE**  | **$19,943** |
| **RMSE** | **$26,412** |
| **MAPE** |   **1.98%** |

The strong test-period fit indicates that monthly cost and encounter volume explain a substantial proportion of the observed variation in the charge-based revenue measure within this dataset.

However, this should not be interpreted as proof of causal relationships.

Cost and charges are inherently connected in healthcare financial activity, and the model contains only a limited number of monthly observations.

---

# Understanding the Regression Results

The model suggests that revenue tends to move with both:

```text
Operational Volume
+
Cost Structure
```

The positive encounter coefficient indicates that higher encounter volume is associated with higher monthly charges, holding cost constant.

The positive cost coefficient similarly indicates that months with higher costs tend to have higher charges, controlling for encounter volume.

These are **conditional statistical associations**, not causal effects.

---

# Six-Month Revenue Forecast

Power BI's forecasting functionality was used to extend the monthly revenue series by six months.

Historical period:

```text
January 2019 – December 2021
36 monthly observations
```

Forecast horizon:

```text
January 2022 – June 2022
```

The forecast includes:

```text
95% confidence intervals
```

which widen as the forecast moves further from the observed data.

This communicates an important reality:

> Future values become increasingly uncertain as the forecast horizon increases.

---

# Forecast Interpretation

The forecast is best viewed as a:

> **short-term planning range rather than a guaranteed prediction.**

Its limitations include:

* only 36 monthly historical observations;
* a relatively short time series;
* a univariate forecasting structure;
* no explicit staffing variables;
* no patient-severity variables;
* no macroeconomic drivers beyond contextual CPI comparison;
* no reimbursement changes;
* no policy shocks; and
* charges being used as a revenue proxy.

---

# Power BI Key Influencers

Power BI's **Key Influencers** visual was used as an AI-assisted diagnostic tool.

Rather than treating the output as causal proof, the analysis uses it as an exploratory mechanism for identifying combinations of attributes associated with changes in healthcare outcomes.

This helps analysts identify where deeper investigation may be warranted.

---

# Prescriptive Analytics

Predictive analytics asks:

> What may happen?

Prescriptive analytics asks:

> What could happen if management changes something?

The project therefore adds interactive **What-If parameters** for:

### Cost Reduction

Allows users to simulate reductions in direct costs.

### Length-of-Stay Reduction

Allows users to estimate the operational effect of reducing average LOS.

Together, these parameters allow management to test alternative operating scenarios interactively.

---

# Selected What-If Scenario

A practical scenario combines:

```text
5% Cost Reduction
+
5% LOS Reduction
```

The model estimates approximately:

| Scenario Metric   |      Result |
| ----------------- | ----------: |
| Estimated Cost    | **$19.78M** |
| Estimated Savings |  **$2.14M** |
| Bed-Days Released |     **572** |
| Estimated Margin  |  **45.50%** |

This scenario was selected as a **controlled pilot scenario**, rather than assuming more aggressive efficiency improvements are automatically achievable.

---

# Interpreting the Prescriptive Scenario

The model does **not** claim that implementing a 5% cost or LOS reduction will automatically produce these results.

The What-If model is assumption-based.

For example, the financial scenario assumes revenue remains constant while cost changes proportionally.

Therefore, the output should be interpreted as:

> **estimated decision-support impact under stated assumptions**

rather than a causal guarantee.

This distinction is essential for responsible prescriptive analytics.

---

# Management Recommendations

Based on the combined descriptive, diagnostic, predictive, and prescriptive analysis, several actions emerge.

### 1. Investigate Imaging-Related Readmissions

The elevated Imaging readmission rate should be reviewed, particularly within the Private payer segment.

Management should investigate:

* discharge quality;
* follow-up scheduling;
* repeat imaging;
* patient severity;
* procedure type;
* diagnosis; and
* time to readmission.

---

### 2. Compare Facility 6 with Better-Performing Facilities

Facility 6's 18.07% readmission rate warrants investigation against lower-rate facilities such as Facility 4.

The comparison should account for:

* procedure mix;
* diagnosis;
* payer mix;
* provider mix;
* case complexity;
* patient severity; and
* transition-of-care processes.

Practices should not be copied between facilities until these differences are understood.

---

### 3. Monitor Financial Performance in Real Terms

Charges should be evaluated alongside Medical Care CPI rather than viewed only in nominal dollars.

This can help distinguish between:

```text
Nominal Financial Change
```

and:

```text
Inflation-Adjusted Financial Performance
```

---

### 4. Track Cost and Margin Together

Cost-reduction initiatives should be evaluated alongside:

* patient outcomes;
* readmission;
* LOS;
* service quality; and
* margin.

Reducing cost without protecting care quality would not represent successful optimization.

---

### 5. Pilot LOS and Cost Improvements

The combined 5% cost / 5% LOS scenario provides a reasonable pilot target for scenario planning.

Actual implementation should be monitored incrementally before larger targets are adopted.

---

# Dashboard Features

The Power BI solution incorporates multiple analytical and UX features, including:

* KPI cards;
* line charts;
* column charts;
* bar charts;
* geographic mapping;
* scatter plots;
* matrices;
* waterfall charts;
* decomposition trees;
* interactive slicers;
* page-level filters;
* bookmarks;
* drill-through;
* navigation buttons;
* What-If parameters;
* Key Influencers;
* forecasting;
* tooltip-based context; and
* dynamic DAX measures.

This provides multiple analytical views while avoiding unnecessary dependence on one visualization type.

---

# Data Governance & Analytical Controls

Several controls are included to improve analytical reliability.

### Sufficient Volume Threshold

Provider and facility comparisons use a minimum-volume threshold where appropriate so that extremely small sample sizes are not overinterpreted.

### Relationship Control

The Power BI model uses a controlled star-schema relationship structure rather than unrestricted bidirectional filtering.

### Dedicated Measures

Major KPIs are implemented as DAX measures rather than duplicated calculations across visuals.

### External Benchmark Separation

Medical Care CPI is maintained as a disconnected benchmark table and integrated intentionally through DAX.

### Non-Causal Interpretation

Observed associations are clearly distinguished from causal relationships.

---

# Repository Structure

The repository is organized into three major stages:

```text
Healthcare-Encounter-Performance-Analytics/
│
├── Part 1/
│   │
│   ├── Data preparation
│   ├── Data profiling
│   ├── Power Query transformations
│   ├── Discharge-date correction
│   ├── Calendar construction
│   ├── Star-schema modelling
│   └── Core DAX measures
│
├── Part 2/
│   │
│   ├── Interactive Power BI dashboard
│   ├── Patient Overview
│   ├── Clinical & Diagnosis Insights
│   ├── Provider & Facility Performance
│   ├── Financial & Payer Analysis
│   ├── Drill-through analysis
│   ├── Decomposition Tree
│   ├── Waterfall analysis
│   └── Medical Care CPI benchmarking
│
├── Part 3/
│   │
│   ├── Predictive analytics
│   ├── Multiple linear regression
│   ├── Revenue forecasting
│   ├── Key Influencers
│   ├── What-If analysis
│   ├── Prescriptive scenarios
│   ├── Interpretation
│   └── Management recommendations
│
└── README.md
```

---

# Tools & Technologies

| Tool                         | Application                                     |
| ---------------------------- | ----------------------------------------------- |
| **Microsoft Power BI**       | Dashboard development and analytical reporting  |
| **Power Query**              | Data cleaning, transformation and ETL           |
| **DAX**                      | Measures, KPIs, calculations and scenario logic |
| **Power BI Forecasting**     | Short-term revenue forecasting                  |
| **Power BI Key Influencers** | AI-assisted diagnostic exploration              |
| **Regression Analysis**      | Predictive revenue modelling                    |
| **Microsoft Excel / CSV**    | Source data storage and staging                 |
| **Git & GitHub**             | Version control and project documentation       |

---

# Skills Demonstrated

## Business Intelligence

* Power BI development
* Dashboard architecture
* Interactive reporting
* KPI design
* Drill-through
* Bookmarks
* Data storytelling

## Data Modelling

* Star schema design
* Fact and dimension modelling
* Relationship management
* Calendar dimensions
* Disconnected tables
* Filter context

## Data Transformation

* Power Query
* Data profiling
* Data-quality validation
* Date correction
* Derived variables
* ETL documentation

## DAX

* Aggregation measures
* Ratio measures
* Filter context
* Time intelligence
* `TREATAS`
* Dynamic scenario calculations
* What-If parameters

## Healthcare Analytics

* Patient utilization
* Healthcare encounters
* Length of stay
* Readmission analysis
* Provider performance
* Facility performance
* Payer analytics
* Healthcare financial performance

## Predictive Analytics

* Multiple linear regression
* Temporal train/test validation
* R²
* MAE
* RMSE
* MAPE
* Time-series forecasting

## Prescriptive Analytics

* Scenario modelling
* Cost optimization
* LOS optimization
* Capacity estimation
* Sensitivity analysis
* Management decision support

---

# Limitations

The findings should be interpreted within the boundaries of the available data.

### Limited Time Period

The primary encounter data span only 2019–2021.

This restricts long-term trend analysis and forecasting reliability.

### Limited Sample Size

The analysis contains 1,500 encounters.

While sufficient for the project, larger operational datasets would support stronger subgroup analysis and more robust predictive modelling.

### No Clinical Severity Adjustment

The dataset does not contain a comprehensive patient-acuity or clinical-severity measure.

As a result, differences between facilities, procedures, providers, or payers may partly reflect differences in patient complexity.

### Limited Comorbidity Information

More detailed comorbidity measures would improve risk-adjusted readmission analysis.

### No Staffing Variables

Provider availability, staffing ratios, workload, and workforce constraints are not included.

### Revenue Proxy

Total Charges are used as the revenue measure because actual collected reimbursement is unavailable.

Therefore:

```text
Charges ≠ Actual Cash Revenue
```

### Readmission Timing

More detailed information about the interval between discharge and readmission would improve clinical interpretation.

### External CPI Benchmark

The Medical Care CPI represents broad U.S. medical-care inflation and is not specific to the healthcare organization represented by this dataset.

### Observational Analysis

Most findings are descriptive or associational.

They should not be interpreted as causal without additional research design and controls.

---

# Future Improvements

Several enhancements could extend the project.

## 1. Risk-Adjusted Readmission Modelling

Add variables such as:

* comorbidities;
* patient acuity;
* prior utilization;
* medication burden;
* emergency admission status; and
* discharge destination.

These variables would support a more defensible readmission-risk model.

---

## 2. Actual Reimbursement Data

Replace billed charges with:

* allowed amounts;
* payments received;
* insurer reimbursement;
* contractual adjustments; and
* patient responsibility.

This would enable true revenue-cycle analysis.

---

## 3. Staffing and Capacity Data

Integrate:

* nurse staffing;
* provider workload;
* bed capacity;
* occupancy;
* wait times; and
* scheduling.

This would strengthen operational-efficiency analysis.

---

## 4. Advanced Predictive Models

Compare the regression baseline with models such as:

* Random Forest;
* Gradient Boosting;
* XGBoost; and
* regularized regression.

These models could help identify nonlinear relationships and interactions.

---

## 5. Readmission Classification

Develop a patient-level model for:

```text
Readmitted
vs.
Not Readmitted
```

with appropriate evaluation measures such as:

* recall;
* precision;
* ROC-AUC;
* F1 score; and
* calibration.

---

## 6. Forecast Backtesting

Evaluate forecast accuracy against held-out historical periods rather than relying only on visual forecast intervals.

---

## 7. Scenario Sensitivity Analysis

Expand What-If modelling to test combinations of:

```text
Cost Reduction
×
LOS Reduction
×
Encounter Growth
×
Revenue Change
```

This would provide a richer planning framework.

---

# Key Takeaway

The main value of this project is not the creation of a dashboard
