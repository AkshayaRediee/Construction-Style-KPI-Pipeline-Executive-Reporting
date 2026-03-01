# Construction-Style-KPI-Pipeline-Executive-Reporting

## Project Controls KPI Pipeline & Executive Dashboard

## Overview

This project demonstrates an end-to-end **Bronze → Silver → Gold data pipeline** built in **Databricks Community Edition** to model construction project controls data and generate executive-level portfolio reporting.

The objective was to simulate a structured PMO / Cost Advisory reporting framework using scalable Lakehouse principles and SQL-based KPI modeling.

The pipeline integrates project master data, cost actuals, schedule updates, and change orders to produce standardized portfolio metrics and risk classification.

All the datasets used are synthetic datasets.

---

## Portfolio Scope

This project models a construction-style portfolio containing:

- **12 total projects**
- **$30,000,000 total baseline budget**
- **$32,635,500 total forecast budget** (baseline + approved change orders)
- **$8,368,575.53 total portfolio cost variance**

Dataset composition:

- 508 cost records  
- 84 schedule updates  
- 44 change orders  
- 4 integrated data sources  

---

## Architecture

The project follows a structured **Bronze → Silver → Gold architecture**.

### Bronze Layer – Raw Ingestion

Raw CSV datasets were loaded into Delta tables:

- `bronze_projects`
- `bronze_cost_actuals`
- `bronze_schedule_updates`
- `bronze_change_orders`

This layer preserves the original data before transformation.

---

### Silver Layer – Data Cleaning & Standardization

The Silver layer performs data validation and transformation:

- Converted string fields to proper `DATE`, `DOUBLE`, and `INT` types  
- Removed null project IDs  
- Filtered negative cost values  
- Standardized change order status (`APPROVED / PENDING / REJECTED`)  
- Applied basic validation rules  

This ensures reliable and consistent KPI calculations.

---

### Gold Layer – Project-Level KPI Mart

A consolidated table `gold_project_kpis` was created to calculate executive metrics at the project level.

#### KPIs Calculated

- Baseline Budget  
- Total Actual Cost  
- Approved Change Orders  
- Total Forecast Budget (Baseline + Approved COs)  
- Cost Variance Amount  
- Cost Variance Percentage  
- Latest Percent Complete  
- Latest Delay Days  
- RAG Risk Classification  

---

## Key Findings

- **$8.36M total portfolio variance exposure identified**
- 1 project with **+28.86% cost overrun**
- 2 projects delayed by 45 days
- Risk classification breakdown:
  - 2 RED projects (16.7%)
  - 4 AMBER projects (33.3%)
  - 6 GREEN projects (50%)

The RAG model was based on defined cost variance and schedule delay thresholds to provide objective portfolio risk visibility.

---

## Executive Dashboard

An Executive Portfolio Dashboard was built in Databricks SQL including:

- Portfolio summary (baseline, actual, forecast, variance)
- Risk distribution (Green / Amber / Red)
- Top overrun projects
- Delay vs cost variance analysis
- Regional portfolio breakdown

The dashboard centralizes portfolio KPIs into a single reporting view.

---

## Technical Implementation

- Databricks Community Edition
- Delta Lake tables
- SQL transformations
- Aggregations and joins
- Window functions (`ROW_NUMBER`)
- Conditional logic (`CASE` statements)

---

## What This Project Demonstrates

- Structured Lakehouse data modeling  
- Multi-source data integration  
- Financial KPI calculation logic  
- Portfolio-level risk assessment  
- Executive-ready reporting design  
- SQL proficiency for analytical modeling  

---

## Limitations

This is a simulated portfolio analytics project built for demonstration purposes.

The following were not implemented:

- Automated job scheduling
- Incremental data loads
- Real stakeholder adoption tracking
- Measured time savings or operational impact

The focus was on demonstrating architecture, KPI logic, and portfolio risk visibility.

---

## Future Enhancements

Potential improvements include:

- Automated scheduled refresh
- Incremental `MERGE` logic
- Forecast modeling (Estimate at Completion prediction)
- Historical variance trend tracking
- Data quality monitoring metrics

---

## Summary

This project models a $30M construction portfolio using a structured Databricks pipeline and produces executive-ready KPIs with risk classification and financial exposure visibility.

It demonstrates practical data engineering, SQL-based KPI modeling, and portfolio-level analytics aligned with PMO and cost advisory reporting frameworks.
