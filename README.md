# Healthcare Utilization Analysis for Dual Enrollees
<p align="center">
  <img src="images2.png" width="300" height="250" allow="autoplay">
  <img src="medi.jpeg" width="300" height="250" allow="autoplay">
</p>

<p>
  <img src="https://img.shields.io/badge/Python_Version-3.10%2B-blue" title="Python Version">
  <img src="https://img.shields.io/github/last-commit/dsrichard97/otherprojects">
  <img src="https://img.shields.io/badge/Financial Analysis-Trends-red">
  <img src="https://img.shields.io/badge/STAT-Time Series-blue">
  <img src="https://img.shields.io/badge/STAT-Causal Inference-blue">
  <img src="https://img.shields.io/badge/Python-Pandas-green">
  <a href="https://github.com/ellerbrock/open-source-badges/"><img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103"></a>

  <p>
  

## Table of Contents
- [Business Problem](#business-problem)
- [Data Source](#data-source)
- [Methods](#methods)
- [Tech Stack](#tech-stack)
- [Authors](#authors)
- [Project Documentation](#project-documentation)

## Business Problem

Current Market:
The healthcare industry faces the critical challenge of managing and reducing hospital readmissions for high-risk patients. A wellness program has been proposed as a potential solution to improve patient health outcomes and reduce the associated costs. The objective of this project is to evaluate the effectiveness of the wellness program in reducing healthcare utilization among individuals who are enrolled in both Medicare and Medicaid, also referred to as dual enrollees.

*Business Problem - Using Causal Inference Proposition*:
A healthcare insurance company wants to understand the impact of a new wellness program designed to reduce hospital readmissions. The company believes that by enrolling high-risk patients in this program, they can improve patient health outcomes and reduce costs associated with readmissions. The business problem is to determine whether the wellness program is effective.

## Data Source

The data used in this project is sourced from state submissions to the Centers for Medicare & Medicaid Services (CMS), as mandated by the Medicare Modernization Act (MMA). These submissions provide monthly snapshot data on dual enrollees, offering insights into the enrollee counts by various eligibility types at both the state and county levels. It's important to note that these figures are not cumulative and represent distinct monthly counts.

<p align="center">
  <img src="prop1.png" width="800" height="250" allow="autoplay">
</p>

## Methods

To understand the impact of the wellness program, we employed several analytical methods:

- **Exploratory Data Analysis (EDA):** Initial data exploration to understand distribution and data integrity.
- **Causal Inference Techniques:** 
  - **Regression Analysis:** To estimate the program's impact on healthcare utilization.
  - **Propensity Score Matching (PSM):** To control for confounding variables and simulate a randomized control trial.
  - **Difference-in-Differences (DiD):** To compare the pre- and post-program changes in utilization.

## Tech Stack

The analysis leverages the following technology stack:

- **Data Wrangling and Analysis:** `Python` with `pandas`, `numpy`, and `statsmodels` for data manipulation and statistical modeling.
- **Data Visualization:** `matplotlib` and `seaborn` for generating informative plots and graphs.
- **Version Control:** `Git` for tracking changes and collaborative development.
- **Hosting/Repository:** `GitHub` for hosting the project repository and documentation.

## Authors

- [dsrichard97](https://github.com/dsrichard97)

## Project Documentation

For a detailed walkthrough of the analysis, including code and visualizations, please refer to the [Healthcare EDA notebook](https://github.com/dsrichard97/Medicare_Dual_Enroll/blob/main/Healthcare_EDA.ipynb).

---
For additional information on the project, installation instructions, usage, and contribution guidelines, please refer to my email.
