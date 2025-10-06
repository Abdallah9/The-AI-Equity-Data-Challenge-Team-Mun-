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



**Othe Data Sources & Methodology Summary**
Our project examines how Artificial Intelligence (AI) reshapes Canada’s labour market, focusing on equity across provinces, demographic groups, and occupations. To achieve this, we integrated Canadian employment data with AI task exposure indices, using an innovative crosswalk across national and international classification systems.

***1. Canadian Employment & Income Data***
We draw primarily on Statistics Canada’s Labour Force Survey (LFS) and Census-based tabulations. These sources provide:
Employment counts (value_x)
! ! !
Demographic breakdowns (province, age, sex, population group, immigrant status)
Income measures (median and average income)
Link: https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1410043801&utm_source=chatgpt.com
https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1410028703&pickMembers%5B0%5D=3.1&pick Members%5B1%5D=4.1&cubeTimeFrame.startMonth=12&cubeTimeFrame.startYear=2024&referenceP
eriods=20241201%2C20241201
https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1410044001&utm_source=chatgpt.com https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=9810064201&utm_source=chatgpt.com

***2. Harmonizing Occupational Codes***
Occupations are classified differently across time and countries. To ensure comparability:
!
We applied the official Statistics Canada concordance file
(NOC 2016 v1.3 → NOC 2021 v1.0).
This harmonization ensures older datasets can be aligned to the latest NOC 2021 structure.
! !
When mappings were one-to-many, we used transparent weighting strategies.
Link:
Correspondence Table: National Occupational Classification (NOC) 2016 V1.3 to National Occupational Classification (NOC) 2021 V1.0 based on GSIM

***3. Linking to NET and SOC Data***
To connect Canadian occupations with international measures:
We used Statistics Canada concordances to map NOC 2021 codes → U.S. SOC codes.
! !
We then linked to the U.S. O*NET database, which provides task-level occupational descriptors.
Link:
https://www.statcan.gc.ca/en/statistical-programs/document/noc2016v1_3-soc2018US

***4. AI Exposure Indices***
We integrated AI exposure indices from recent labour economics and computer science research, including:
Webb (2020) – linking AI capabilities to O*NET tasks
! ! !
Felten et al. – measuring automation and augmentation potential
AIOE Data Appendix – consolidated AI occupation exposure estimates
Link:
AIOE/AIOE_DataAppendix.xlsx at main · AIOE-Data/AIOE

***5. Employment-Weighted AI Exposure***
Finally, we computed employment-weighted exposure scores:
AI_Exposure_group = ( Σ (employment × ai_exposure) ) / ( Σ employment )
This provides equity-aware insights: which provinces, groups, and occupations face higher AI disruption risks, and where opportunities may emerge.

**Summary**
By integrating Canadian employment data, official occupational concordances, U.S. task data, and AI exposure indices, we built a unique dataset that illuminates AI’s potential impact on Canada’s workforce. This approach balances credibility, innovation, and accessibility, aligning strongly with the competition’s evaluation criteria.



Final Data can be found here (Insde final_data_parquet): https://1drv.ms/f/c/d2ea6cbbe5e14963/ElMCe16P-41IlrKaYwEVOgEBcyqMYHb922Q4zkbOnsg7FA?e=SIWAML





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




































