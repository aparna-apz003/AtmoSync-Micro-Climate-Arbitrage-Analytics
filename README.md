# 🥑 AtmoSync — Micro-Climate Arbitrage Analytics

Team Members:

Aparna c
Mameeth C
Malavika Nair
Lucky Aswal
    

Infotact Data Analytics Project | Progress & Status Report

Real-time IoT sensor analytics to detect in-transit commodity spoilage and identify profitable reroute ("arbitrage") opportunities before goods degrade below quality thresholds.

Python Pandas Status License 

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![Status](https://img.shields.io/badge/Status-Week%201%20Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Project Overview

Traditional supply chain analytics rely on standard transit times and macro-weather forecasts — they miss hyper-local micro-climate shifts (e.g. a humidity spike inside one specific container) that quietly spoil agricultural cargo before it reaches market.

**AtmoSync** simulates a live IoT sensor pipeline for refrigerated shipping containers, calculates a real-time **spoilage risk score**, and flags **"Spoilage Arbitrage"** opportunities — cases where rerouting a container to a closer secondary market preserves more value than pushing on to the original destination.The core of this analysis relies on rigorous data cleaning and validation protocols to ensure these real-time risk scores remain highly accurate.

This repository documents my work as the **Data Analyst** on the project (data engineering tools like Kafka/Snowflake/dbt/Superset were out of scope — this build uses Python + pandas + Excel instead, to match an analyst's toolkit).

---

Week 1 — Data Foundations & EDA
#	Task	Status
1	Defined dataset schema (sensor, logistics, and pricing fields)	✅ Done
2	Generated 50,000-row synthetic IoT dataset (550 containers × ~91 readings)	✅ Done
3	Performed 9-step data cleaning process & business-rule validation	✅ Done
4	Conducted initial Exploratory Data Analysis (EDA) on spoilage factors	✅ Done
5	Compiled findings into stakeholder-ready reports	✅ Done

---

## 🗂️ Dataset Summary

| Property | Value |
|---|---|
| Total sensor readings | 50,000 |
| Containers tracked | 550 |
| Commodities covered | Avocado, Banana, Mango, Strawberry, Tomato, Grapes, Blueberry |
| Reading frequency | Every 30 minutes across a ~50-hour transit journey |
| Time span | Last 60 days |
| Data completeness | 100% (0 missing values) |
| Duplicate records | 0 |

**Key columns:**
- **Sensor data:** `temperature_c`, `humidity_pct`, `vibration_g`
- **Derived health metrics:** `quality_score`, `temp_deviation_c`, `shelf_life_hours_remaining`
- **Logistics:** `origin_port`, `primary_market`, `secondary_market`, `distance_primary_km`, `distance_secondary_km`
- **Financials:** `primary_price_per_kg_usd`, `secondary_price_per_kg_usd`, `arbitrage_gain_usd`
- **Decision output:** `risk_status` (Normal / Watch / At-Risk / Critical), `recommended_action`

---

## 🧹 Data Cleaning Process (Python / pandas)

All 9 steps were run against the raw dataset before analysis:

```python
import pandas as pd

# 1. Load & inspect
df = pd.read_csv("atmosync_dataset.csv")
df.shape, df.info()

# 2. Missing values
df.isnull().sum()

# 3. Duplicates
df.duplicated().sum()

# 4. Fix data types
df["timestamp"] = pd.to_datetime(df["timestamp"])
df["commodity"] = df["commodity"].astype("category")

# 5. Standardize text
df["origin_port"] = df["origin_port"].str.strip()

# 6. Validate business rules
(df["quality_score"] < 0).sum()
(df["quality_score"] > 100).sum()

# 7. Flag (not delete) genuine outlier events
df["data_quality_flag"] = "Normal Reading"
df.loc[df["temp_deviation_c"] > 3, "data_quality_flag"] = "Significant Temperature Drift"

# 8. Cross-column consistency checks
(df["ideal_temp_min_c"] >= df["ideal_temp_max_c"]).sum()

# 9. Export cleaned file
df.to_csv("atmosync_dataset_CLEANED.csv", index=False)
```

**Cleaning results:**

| Check | Result |
|---|---|
| Missing values | 0 |
| Duplicate rows | 0 |
| Business-rule violations (negative values, out-of-range scores, future timestamps) | 0 |
| Outlier readings flagged (not deleted) | 3,647 (7.3%) |
| Final dataset | 50,000 rows × 31 columns (certified clean) |

> **Design decision:** Outlier sensor readings were **flagged**, not deleted. In this dataset, an unusual reading *is* the spoilage signal the business needs — deleting it would hide the exact problem the project exists to detect.

---

## 📊 Key Findings (Week 1 EDA)

- **83%** of containers are currently Normal; **13%** (74 containers) are At-Risk or Critical and need a routing decision.
- **Temperature deviation** has a strong negative correlation with quality score (**r = -0.84**) — it's the single biggest driver of spoilage, far more than humidity or vibration.
- **Faulty cooling units** (18.5% of containers) are the root cause of nearly all serious spoilage: average quality score of **40.5** vs. **96.6** for healthy units.
- **Strawberries, grapes, and blueberries** are the most climate-sensitive commodities; **tomatoes** are the most forgiving.
- **$538,693** worth of cargo is currently tied up in At-Risk/Critical containers; rerouting the right containers now would capture an estimated **$120,533** in additional value.
- Commodity Variance: For highly sensitive goods like strawberries and blueberries, this critical action window shrinks to under 8 hours before total loss

*(Full analysis with charts: see `/reports/AtmoSync_Data_Findings_Report.pdf`)*

---

## 🛠️ Tools Used



| Purpose | Tool |
|---|---|
| Data generation & manipulation | Python, pandas, numpy |
| Data cleaning & validation | pandas |
| Exploratory analysis & statistical modeling | pandas (`groupby`, `corr`, `value_counts`) |
| Visualizations & Dashboards | matplotlib, seaborn |
| Executive Presentation | Microsoft PowerPoint (`AtmoSync.pptx`) |
| Version control | Git & GitHub |

---


---

## 📁 Repository Structure

```
atmosync-analytics/
│
├── data/
│   ├── atmosync_dataset.csv              # Raw dataset (50,000 rows)
│   └── atmosync_dataset_CLEANED.csv      # Cleaned & validated dataset
│
├── notebooks/
│   └── week1_eda_and_cleaning.ipynb      # Full cleaning + EDA workflow
│
├── reports/
│   ├── AtmoSync_Data_Cleaning_Report.pdf # Cleaning process, stakeholder statements
│   └── AtmoSync_Data_Findings_Report.pdf # EDA findings with charts
│
├── scripts/
│   ├── generate_dataset.py               # Synthetic dataset generator
│   └── clean_data.py                     # Cleaning pipeline
│
└── README.md
```

---

## 🚀 How to Run This Project

```bash
# Clone the repo
git clone https://github.com/Mameeth-4015/atmosync-analytics.git
cd atmosync-analytics

# Install dependencies
pip install pandas numpy matplotlib seaborn

# Run the cleaning pipeline
python scripts/clean_data.py

# Open the analysis notebook
jupyter notebook notebooks/week1_eda_and_cleaning.ipynb
```

---

## 📅 Coming in Week 2

- [ ] Build baseline visual dashboards (temperature trends, container routes)
- [ ] Deeper spoilage-curve modeling per commodity
- [ ] Merge historical commodity pricing trends
- [ ] Begin Excel/Power BI-style dashboard mockup for stakeholder review

---

## 👤 Author

**Data Analyst — AtmoSync Project**
GitHub: [@Mameeth-4015](https://github.com/Mameeth-4015)
