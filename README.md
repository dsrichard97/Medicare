# Healthcare Utilization Analysis for Dual Enrollees

<p align="center">
  <img src="images2.png" width="300" height="250" />
  <img src="medi.jpeg" width="300" height="250" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python_Version-3.10%2B-blue" alt="Python Version">
  <img src="https://img.shields.io/badge/SQL-blue" alt="Google BigQuery">
  <img src="https://img.shields.io/github/last-commit/dsrichard97/otherprojects" alt="Last Commit">
  <img src="https://img.shields.io/badge/Financial_Analysis-Trends-red" alt="Financial Analysis">
  <img src="https://img.shields.io/badge/STAT-Time_Series-blue" alt="Time Series">
  <img src="https://img.shields.io/badge/STAT-Causal_Inference-blue" alt="Causal Inference">
  <img src="https://img.shields.io/badge/Python-Pandas-green" alt="Pandas">
  <a href="https://github.com/ellerbrock/open-source-badges/">
    <img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103" alt="Open Source">
  </a>
</p>

## Table of Contents
- [Business Problem](#business-problem)
- [Data Source](#data-source)
- [Methods](#methods)
- [Tech Stack](#tech-stack)
- [Authors](#authors)
- [Project Documentation](#project-documentation)
- [SQL Code](#sql-code)

## Business Problem

**Context in the Healthcare Sector:**
The healthcare industry currently grapples with the significant issue of reducing hospital readmissions, particularly for high-risk patients. A wellness program has been suggested as a potential strategy to enhance patient health outcomes while concurrently cutting down on related expenses. This project's goal is to assess how effective the wellness program is in diminishing healthcare usage among individuals who participate in both Medicare and Medicaid, often known as dual enrollees.

**Business Challenge - Leveraging Causal Inference for Strategic Insights:**
Gaining a deeper understanding of dual enrollees is crucial for businesses, especially in strategizing marketing efforts to attract new memberships. Typically, account managers or sales teams work on a contractual basis with businesses. In some cases, they focus on tracking specific members to not only boost memberships but also to develop more effective marketing strategies. This project aims to provide a comprehensive overview of dual enrollees from a causal inference standpoint, offering valuable insights for targeted business strategies.

## Data Source
**Data Origin and Regulatory Background: ** 
The data for this project is derived from submissions made by states to the Centers for Medicare & Medicaid Services (CMS), as required under the Medicare Modernization Act (MMA). These submissions are a critical source of information, as they furnish monthly snapshot data on individuals enrolled in both Medicare and Medicaid.

**Nature of the Data: ** 
The provided data offers valuable insights into the number of dual enrollees, categorized by various eligibility criteria at both state and county levels. A crucial aspect to understand is that these numbers are not cumulative; they represent unique counts for each month. This distinction is vital for accurate analysis and interpretation of trends over time.

**Data Processing and Analysis Tools: ** 
For data processing and analysis, SQL code is utilized, specifically leveraging the capabilities of Google BigQuery. Google BigQuery's robust platform allows for efficient handling and analysis of large datasets, making it an ideal tool for extracting meaningful patterns and conclusions from the CMS data. For a sample overview of the whole code: 

## Methods - Causal inference (Initial Snooping)

<p align="center">
  <img src="prop1.png" width="600" height="200" />
</p>

To understand the impact of the wellness program, we employed several analytical methods:

<p align="center">
  <img src="prop2.png" width="600" height="200" />
</p>

### Causal Inference Techniques
- **Exploratory Data Analysis (EDA):** Initial data exploration to understand distribution and data integrity.
<p align="center">
  <img src="init.png" width="400" height="200" />
</p>

- **Regression Analysis**: Utilized for estimating the impact of a program on healthcare utilization metrics.
- **Propensity Score Matching (PSM)**: Employed to adjust for confounders and emulate the conditions of a randomized controlled trial, thereby approximating the causal effect of the program.
- **Difference-in-Differences (DiD)**: Applied to assess the differential effect of the program by comparing the changes in healthcare utilization before and after the program's implementation, across treatment and control groups.

## Recommendations

<p align="center">
  <img src="prop3.png" width="400" height="200" />
</p>

**Methods Performed:**

1. **Causal Inference with Regression:**
   Attempted to estimate the treatment effect using regression.
   Results indicated no significant treatment effect.

2. **Temporal Causal Inference:**
   - **Interrupted Time Series (ITS):** Considered but not implemented due to data constraints.
   - **Difference-in-Differences (DiD):** Implemented to estimate the treatment effect over time.

**Regression Model Results:**

<p align="center">
  <img src="init2.png" width="300" height="200" />
</p>

Initial OLS regression showed no explanatory power.
P-values for the treatment effect were non-significant, suggesting model reassessment is needed.

**Follow-Up Analysis:**

- Consider more granular data collection.
- Explore additional analytical methods.
- Assess the need for more robust control groups.

## Tech Stack
- **Data Wrangling and Analysis:** `Python` with `pandas`, `numpy`, and `statsmodels` for data manipulation and statistical modeling.
- **Data Visualization:** `matplotlib` and `seaborn` for generating informative plots and graphs. [Tableau](https://public.tableau.com/views/MedicareDualEnrollment2015-18/Dashboard3?:language=en-US&:display_count=n&:origin=viz_share_link)
- **Version Control:** `Git` for tracking changes and collaborative development.
- **Hosting/Repository:** `GitHub` for hosting the project repository and documentation.

## Authors

- [dsrichard97](https://github.com/dsrichard97)

## Project Documentation

For a detailed walkthrough of the analysis, including code and visualizations, please refer to the [Healthcare EDA notebook](https://github.com/dsrichard97/Medicare_Dual_Enroll/blob/main/Healthcare_EDA.ipynb).


## SQL Code

```sql
WITH CleanedData AS (
    SELECT 
        State_Abbr,
        County_Name,
        Date,
        COALESCE(QMB_Only, 0) AS Total_QMB_Only, --using COALESCE to fill with 0 for null values
        COALESCE(QMB_plus_Full, 0) AS Total_QMB_plus_Full,
        COALESCE(SLMB_only, 0) AS Total_SLMB_only,
        COALESCE(SLMB_plus_Full, 0) AS Total_SLMB_plus_Full,
        COALESCE(QDWI, 0) AS Total_QDWI,
        COALESCE(QI, 0) AS Total_QI,
        COALESCE(Other_full, 0) AS Total_Other_full,
        COALESCE(Public_Total, 0) AS Total_Public_Total
    FROM 
`bigquery-public-data.sdoh_cms_dual_eligible_enrollment.dual_eligible_enrollment_by_county_and_program`
)
SELECT
    State_Abbr,
    County_Name,
    Date,
    SUM(Total_QMB_Only) AS Total_QMB_Only,
    SUM(Total_QMB_plus_Full) AS Total_QMB_plus_Full,
    SUM(Total_SLMB_only) AS Total_SLMB_only,
    SUM(Total_SLMB_plus_Full) AS Total_SLMB_plus_Full,
    SUM(Total_QDWI) AS Total_QDWI,
    SUM(Total_QI) AS Total_QI,
    SUM(Total_Other_full) AS Total_Other_full,
    SUM(Total_Public_Total) AS Total_Public_Total
FROM
    CleanedData
GROUP BY
    State_Abbr,
    County_Name,
    Date
ORDER BY
    State_Abbr,
    County_Name,
    Date;

