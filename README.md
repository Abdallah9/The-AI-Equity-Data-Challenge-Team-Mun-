# The AI Equity Data Challenge (Team MUN)
As artificial intelligence continues to transform industries in Canada, it’s reshaping the future of work in record time. But who stands to gain the most, and who might be left behind? 

---

# 📊 Data Preparation and Sources

Our analysis draws on three complementary datasets covering **wages, employment, and demographics** in Canada between 2015 and 2024. Below we document how each dataset was obtained, examined, and cleaned.

---

## 1. Job Bank Wages (2015–2024)

* **Source:** [Job Bank Canada – Wages by Occupation](https://www.jobbank.gc.ca/trend-analysis/search-wages)
* **Raw form:** Individual yearly CSVs (`jobbank_wages_2015.csv` … `jobbank_wages_2024.csv`).
* **Initial issues:**

  * Many columns contained only `NaN` values, except for `year` and `median_wage_hourly`.
  * Annual vs. hourly wage inconsistencies.
* **Processing steps:**

  * Unified column names: `year, noc, occupation_title, province, wage_hourly`.
  * Converted **annual wages** into hourly equivalents for consistency.
  * Stacked yearly files into one dataset covering 2015–2024.
* **Final output:** `jobbank_wages_2015_2024_hourly_cleaned.csv`
* **Purpose:** Provides **wage trends by occupation and province**, critical for analyzing wage equity under AI-driven labour changes.

---

## 2. Labour Force Survey (LFS) – Employment by Occupation (2015–2024)

* **Source:** [Statistics Canada Table 14-10-0310-01 (formerly CANSIM 282-0155)](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1410031001)
* **Raw form:** Large CSV with monthly employment counts across occupations and provinces.
* **Initial issues:**

  * Included multiple statistics (e.g., standard errors, confidence intervals).
  * Needed harmonization across provinces and years.
* **Processing steps:**

  * Filtered to keep **employment estimates only**.
  * Converted monthly values → **annual averages** (mean of 12 months).
  * Standardized provinces (`ON, QC, NL…`) and occupations (`noc`).
* **Final output:** `LFS_employment_by_occupation_2015_2024_clean.csv`
* **Purpose:** Captures **labour demand and job distribution by occupation**, aligning with wage data to show supply/demand shifts.

---

## 3. Labour Force Survey (LFS) – Demographics (2015–2024)

* **Source:** [Statistics Canada Table 14-10-0088-01 – Labour force characteristics of immigrants by country of birth](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1410008801)
* **Raw form:** Detailed CSV with employment, participation, and unemployment rates by:

  * Immigrant status,
  * Country of birth,
  * Sex,
  * Age group.
* **Initial issues:**

  * Dataset was wide and complex, requiring restructuring.
  * Some variables irrelevant to our scope.
* **Processing steps:**

  * Extracted only **Employment rate, Participation rate, Unemployment rate**.
  * Standardized columns: `year, province, immigrant_status, country_of_birth, sex, age_group, lf_characteristic, value`.
  * Cleaned missing values (\~1% of entries).
* **Final output:** `LFS_demographics_2015_2024_clean.csv`
* **Purpose:** Provides **demographic insights** (immigrants vs Canadian-born, gender, age cohorts), enabling analysis of **diversity, inclusion, and equity** in employment outcomes.

---

## Why These Three Datasets?

Together, these datasets give a **multi-dimensional view of the Canadian labour market**:

* **Wages (Job Bank):** How pay differs by occupation and province.
* **Employment by Occupation (LFS):** Which jobs are growing or declining.
* **Demographics (LFS):** Who benefits (or is excluded) from employment opportunities (immigrants, women, younger workers, etc.).

This integrated framework allows us to address questions on:

* Wage equity,
* Regional and occupational skill gaps,
* Demographic impacts of AI adoption.

