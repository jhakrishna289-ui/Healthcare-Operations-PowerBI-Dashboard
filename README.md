# Healthcare-Operations-PowerBI-Dashboard
An interactive 2-page Power BI Dashboard for Healthcare Optimization.
# 🏥 Clinical Operations & Financial Optimization Dashboard

An end-to-end Business Intelligence project developed in **Power BI** utilizing a healthcare dataset of 10,000 patient admissions. This dashboard analyzes hospital operational efficiency, clinical outcomes, and financial billing performance.

## 📊 Live Dashboard Preview
*(Add your dashboard screenshots here)*

---

## 🎯 Project Objectives
- Optimize hospital financial metrics by understanding revenue drivers.
- Analyze patient demographics (Age, Medical Conditions) to evaluate clinical workloads.
- Assess operational efficiency via patient length of stay (LOS) trackers.

---

## 🧹 Data Cleansing & ETL Pipeline (Power Query)
The raw dataset contained significant data anomalies and text corruptions. The following transformations were executed in Power Query to ensure data integrity:
- **Age Standardization:** Fixed text corruptions where `I` replaced `1` (e.g., `8I` converted to `81`) and cast the column to a Whole Number.
- **Billing Correction:** Handled alphanumeric glitches where the character `O` replaced `0` (e.g., `6452O` converted to `$64,520`) and cast to Fixed Decimal.
- **Text Normalization:** Standardized mixed casing for medical conditions (e.g., merging `ARTHRITIS` and `hypertension` into proper capitalized words).
- **Trim & Clean:** Removed trailing whitespace and corrected text padding errors across the `Admission Type` column.

---

## 🧬 Data Modeling & Advanced DAX Formulas
Custom calculations were built to enrich the clinical analysis:

1. **Length of Stay (Calculated Column):** Evaluates how many days a patient occupied a hospital bed.
   ```dax
   Length of Stay = DATEDIFF('healthcare_data'[Date of Admission], 'healthcare_data'[Discharge Date], DAY)
   ```

2. **Age Demographic Grouping (Calculated Column):** Segments patient volume by life stage.
   ```dax
   Age Group = 
   SWITCH(
       TRUE(),
       'healthcare_data'[Age] <= 18, "0-18 (Children)",
       'healthcare_data'[Age] <= 35, "19-35 (Youth)",
       'healthcare_data'[Age] <= 60, "36-60 (Adults)",
       "60+ (Seniors)"
   )
   ```

3. **Average Cost Per Day (Measure):** Calculates financial yield per bed-day allocated.
   ```dax
   Avg Cost Per Day = 
   VAR TotalBilling = SUM('healthcare_data'[Billing Amount])
   VAR TotalStay = SUM('healthcare_data'[Length of Stay])
   RETURN
   DIVIDE(TotalBilling, TotalStay, 0)
   ```

---

## 📈 Key Insights & Analytical Outcomes
- **Financial Driver:** **Cancer** constitutes the highest overall hospital billing volume, exceeding \$70M in aggregate revenue.
- **Operational Strain:** The average length of stay across all conditions is **13.8 days**, highlighting extended hospital resource allocation.
- **Diagnostic Load:** **Abnormal lab results** comprise the highest single category of clinical test outcomes (34.56%).
- **Insurance Contribution:** Medicare and Blue Cross lead the financial settlement streams, accounting for over 43% of total revenue.

---

## 📁 Repository Structure
- `healthcare_data.csv`: The raw dataset used for this project.
- `Healthcare_Optimization_Dashboard.pbix`: The complete Power BI Desktop file containing data models, Power Query M-code, and the visual dashboard.

---
*Developed as part of my Data Analytics Portfolio to demonstrate corporate-level BI readiness.*
