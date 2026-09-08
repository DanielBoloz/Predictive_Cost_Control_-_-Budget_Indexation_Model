# Predictive_Cost_Control_-_-Budget_Indexation_Model

## 📌 Project Overview
This project is an automated Business Intelligence solution built for **Project Controls and Cost Analysis** in heavy infrastructure investments. It demonstrates the ability to dynamically index a baseline construction budget against real-time macroeconomic indicators (Eurostat PPI), effectively calculating inflation-driven cost variances (Claims/EVM). 

The architecture strictly follows the requirements typically outlined in a standard "Project Controls - Job Offer", focusing on automated ETL pipelines, relational data modeling, and advanced DAX business logic.

## 🏗️ Technical Architecture & Stack
* **Environment:** Microsoft Power BI Desktop
* **Data Engineering (ETL):** Power Query (M-Code)
* **Data Modeling:** Relational Star Schema (1-to-Many relationships)
* **Business Logic:** DAX (Iterators, Time Intelligence)
* **Source Data:** Eurostat Database (Indicator: `sts_inppd_m`, C24.1 EU27) & Project Baseline (Excel)

## ⚙️ Execution Phases

### 1. Data Engineering (ETL)
Extracted over multiple historical data points directly from Eurostat. The raw data underwent a rigorous cleaning process in Power Query:
* **Anomaly Extermination:** Automated removal of text flags (e.g., Eurostat's "e" or ":" missing values) from numeric columns to prevent VertiPaq engine errors.
* **Data Typing & Localization:** Forced structural decimal data typing bypassing regional conflict errors.
* **Fact & Dimension Isolation:** Separated raw data into dedicated Fact Tables (`Fact_Steel_Budget`, `Fact_Steel_PPI`).

### 2. Data Modeling (Star Schema)
Built a highly optimized relational data model avoiding direct Many-to-Many relationships:
* Implemented a continuous `Dim_Calendar` (Date Table) generated entirely via DAX to act as the central nervous system of the model.
* Established unidirectional, 1-to-Many filtering paths from the Calendar to both Fact tables to enable dynamic time-based indexing.

### 3. Business Logic (DAX & EVM)
Translated standard Earned Value Management (EVM) methodology into automated DAX measures:
* **Planned Value (PV):** `1_Baseline_Budget` calculated via the `SUMX` iterator, multiplying baseline structural tonnage by a fixed base price.
* **Indexation Engine:** `2_PPI_Multiplier` dynamically converting the EU27 Producer Price Index (2021=100) into a mathematical multiplier based on the active time filter context.
* **Actual Cost (AC):** `3_Indexed_Actual_Cost` forcing row-by-row revaluation of the steel budget against historical market inflation.
* **Cost Variance (CV):** `4_Cost_Variance` isolating the exact financial loss/gain driven strictly by market volatility, providing hard evidence for claim management.

### 4. UI/UX & Visualization
* **Design Pattern:** Dark mode layout focusing purely on analytical clarity (no pastel colors or pie charts).
* **Waterfall Chart:** Cascading breakdown of Cost Variance over time, instantly showing exactly when and where the project started bleeding cash.
* **S-Curve Dynamics:** Line charts visualizing the divergence between the flat baseline budget and the volatile indexed actual costs.

## 🔒 Security Note
This repository contains only the `.pbit` (Power BI Template) file. Raw financial and baseline data are intentionally excluded from the public repository in compliance with standard corporate Data Governance protocols.
