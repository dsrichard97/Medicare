# Healthcare Utilization Analysis for Dual Enrollees

<div align="center">
  <img src="images2.png" width="300" height="250" alt="Healthcare Utilization Image 1">
  <img src="medi.jpeg" width="300" height="250" alt="Healthcare Utilization Image 2">
</div>

<div align="center">
  <img src="https://img.shields.io/badge/Python_Version-3.10%2B-blue" alt="Python Version">
  <img src="https://img.shields.io/github/last-commit/dsrichard97/otherprojects" alt="Last Commit">
  <img src="https://img.shields.io/badge/Financial Analysis-Trends-red" alt="Financial Analysis - Trends">
  <img src="https://img.shields.io/badge/STAT-Time Series-blue" alt="STAT - Time Series">
  <img src="https://img.shields.io/badge/STAT-Causal Inference-blue" alt="STAT - Causal Inference">
  <img src="https://img.shields.io/badge/Python-Pandas-green" alt="Python - Pandas">
  <a href="https://github.com/ellerbrock/open-source-badges/">
    <img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103" alt="Open Source Badge">
  </a>
</div>

## Table of Contents
- [Introduction](#introduction)
- [Business Problem](#business-problem)
- [Data Source](#data-source)
- [Methodology](#methodology)
- [Causal Inference Techniques](#causal-inference-techniques)
- [Recommendations](#recommendations)
- [SQL Queries](#sql-queries)
- [Tech Stack](#tech-stack)
- [Authors](#authors)
- [Project Documentation](#project-documentation)

## Introduction
<p align="justify">
The healthcare industry is facing the critical challenge of managing and reducing hospital readmissions for high-risk patients. This project aims to evaluate the effectiveness of a wellness program in reducing healthcare utilization among dual enrollees in Medicare and Medicaid, using a rigorous data-driven approach.
</p>

## Business Problem
<p align="justify">
A healthcare insurance company seeks to understand the impact of a new wellness program aimed at reducing hospital readmissions. By analyzing patient data, the company aims to improve health outcomes and reduce costs, establishing the efficacy of the program.
</p>

## Data Source
<p align="justify">
Data for this analysis is sourced from state submissions to the Centers for Medicare & Medicaid Services (CMS), providing valuable insights into enrollee counts by eligibility types on a monthly basis.
</p>

## Methodology
<div align="center">
  <img src="prop1.png" width="600" height="200" alt="Methodology Visual">
</div>

## Causal Inference Techniques
- **Regression Analysis:** Estimating program impact on healthcare utilization.
- **Propensity Score Matching (PSM):** Simulating randomized control trials to control confounding variables.
- **Difference-in-Differences (DiD):** Assessing pre- and post-program changes in utilization.

## Recommendations
<div align="center">
  <img src="prop3.png" width="400" height="200" alt="Recommendations Visual">
</div>

## SQL Queries
```sql
-- Example SQL query to analyze healthcare data
SELECT patient_id, program_enrollment, hospital_visits
FROM healthcare_utilization
WHERE program_enrollment = 'Wellness Program'
GROUP BY patient_id
ORDER BY hospital_visits DESC;
