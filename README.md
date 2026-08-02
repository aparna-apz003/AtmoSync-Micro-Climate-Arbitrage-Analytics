# 🥑 AtmoSync — Micro-Climate Arbitrage Analytics

**Team Members:**
* Aparna C
* Mameeth C
* Malavika Nair
* Lucky Aswal

**Infotact Data Analytics Project | Progress & Status Report**

> Real-time IoT sensor analytics to detect in-transit commodity spoilage and identify profitable reroute ("arbitrage") opportunities before goods degrade below quality thresholds.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811)
![Status](https://img.shields.io/badge/Status-Week%203%20Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Project Overview

Traditional supply chain analytics rely on standard transit times and macro-weather forecasts — they miss hyper-local micro-climate shifts (e.g. a humidity spike inside one specific container) that quietly spoil agricultural cargo before it reaches market.

**AtmoSync** simulates a live IoT sensor pipeline for refrigerated shipping containers, calculates a real-time **spoilage risk score**, and flags **"Spoilage Arbitrage"** opportunities — cases where rerouting a container to a closer secondary market preserves more value than pushing on to the original destination.

This repository documents our work as the **Data Analytics Team** on the project, using Python, pandas, data visualizations, Power BI, and executive presentation materials to build actionable business insights.

---

## ✅ Progress Tracking

### Week 1 — Data Foundations & EDA
| # | Task | Status |
|---|------|--------|
| 1 | Defined dataset schema (sensor, logistics, and pricing fields) | ✅ Done |
| 2 | Generated 50,000-row synthetic IoT dataset (550 containers × ~91 readings) | ✅ Done |
| 3 | Performed 9-step data cleaning process & business-rule validation | ✅ Done |
| 4 | Conducted initial Exploratory Data Analysis (EDA) on spoilage factors | ✅ Done |
| 5 | Compiled findings into stakeholder-ready reports | ✅ Done |

### Week 2 — Dashboard Visualizations & In-Depth Modeling
| # | Task | Status |
|---|------|--------|
| 1 | Generated baseline temperature tracking & anomaly distribution visuals | ✅ Done |
| 2 | Modeled quality degradation across specific commodities and transit hours | ✅ Done |
| 3 | Mapped risk status severity against automated action workflows | ✅ Done |
| 4 | Evaluated multi-metric correlation matrix for micro-climate factors | ✅ Done |
| 5 | Performed market price comparisons for micro-climate arbitrage | ✅ Done |

### Week 3 — Power BI Dashboard Development & Deployment
| # | Task | Status |
|---|------|--------|
| 1 | Imported and modeled `cleaned_dataset.csv` in Power BI (Power Query cleanup, date/time parsing, Date dimension table) | ✅ Done |
| 2 | Built core DAX measure library (volume, environmental, quality/shelf-life, risk, and financial/arbitrage measures) | ✅ Done |
| 3 | Designed **Executive Overview** page — fleet-wide KPIs, risk distribution, origin-port map | ✅ Done |
| 4 | Designed **Environmental Monitoring** page — temperature/humidity drift trends over transit hours, temp-vs-vibration scatter analysis, flagged-container watchlist | ✅ Done |
| 5 | Designed **Risk & Alerts** page — live risk matrix with latest-status-per-container logic, faulty cooling unit tracking | ✅ Done |
| 6 | Designed **Financial / Arbitrage Analysis** page — primary vs. secondary market value comparison, reroute-opportunity breakdown by commodity | ✅ Done |
| 7 | Built **Container Detail** drill-through page for single-shipment sensor history | ✅ Done |
| 8 | Applied conditional formatting & consistent risk-status color theme across all pages | ✅ Done |
| 9 | Documented full build process (step-by-step guide + DAX reference) for handoff | ✅ Done |

---

## 📊 Key Findings & Visual Insights (Week 2)

### 1. Temperature Control & Drift Tracking
* **Trace Analysis (`chart1_temperature_trace.png`):** Real-time monitoring shows distinct containers exceeding safe thermal limits during mid-transit.
* **Deviation Distribution (`chart2_temp_deviation_hist.png`):** Temperature variance strongly skews right, confirming that localized cooling unit failures cause severe thermal spikes.

### 2. Commodity Spoilage & Quality Modeling
* **Quality by Commodity (`chart3_quality_by_commodity.png`):** High-sensitivity commodities (Strawberries, Blueberries) exhibit significantly sharper quality loss when exposed to thermal shifts compared to hardier cargo like Tomatoes.
* **Transit Duration vs. Quality (`chart4_quality_vs_transit_scatter.png`):** Demonstrates a direct inverse correlation between total transit hours and container quality retention, accelerating rapidly after temperature breach events.

### 3. Risk Assessment & Arbitrage Potential
* **Risk & Action Distribution (`chart5_risk_and_action_counts.png`):** Categorizes fleet status across *Normal*, *Watch*, *At-Risk*, and *Critical* states to trigger automated rerouting actions.
* **Metric Correlations (`chart6_correlation_heatmap.png`):** Reaffirms that `temp_deviation_c` holds the strongest negative correlation ($r = -0.84$) with `quality_score`.
* **Price Arbitrage Comparison (`chart7_price_comparison.png`):** Highlights market price differentials between primary and secondary ports, supporting real-time rerouting decisions to maximize recovered value.

---
## 🚀 Installation & Setup

To replicate this project locally:

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-username/atmosync-analytics.git](https://github.com/your-username/atmosync-analytics.git)
   cd atmosync-analytics
   pip install pandas numpy matplotlib seaborn jupyter

## 📊 Key Findings & Visual Insights (week 3)

### 1. From Static Charts to a Live Decision Tool
* Week 2's matplotlib/seaborn analysis confirmed *what* drives spoilage risk; Week 3 turned those findings into a **self-service Power BI dashboard** that operations staff can filter, drill into, and monitor without needing Python or notebooks.

### 2. Fleet-Wide Risk Visibility
* The **Executive Overview** page surfaces, at a glance, how many of the 550 active containers are currently `At-Risk` or `Critical`, and which commodities are disproportionately affected — directly operationalizing the Week 2 correlation findings.

### 3. Root-Cause Drill-Down
* The **Environmental Monitoring** page's temperature-vs-vibration scatter and drift watchlist make it possible to distinguish *cooling-unit failures* from *rough-handling events* as separate spoilage causes, rather than treating all temperature deviation as one category.

### 4. Real-Time Arbitrage Decisioning
* The **Financial / Arbitrage Analysis** page converts the Week 2 price-comparison findings into an actionable per-container view — ranking shipments by `arbitrage_gain_usd` so the highest-value rerouting opportunities are immediately visible, with `Containers Favoring Secondary Market` quantifying how many shipments per commodity would benefit from rerouting today.

### 5. Single-Shipment Traceability
* The **Container Detail** drill-through page closes the loop from fleet-level insight down to one container's full sensor timeline, supporting audit and incident-review use cases.

---

## 🛠️ Tools Used

| Purpose | Tool |
|---|---|
| Data generation & manipulation | Python, pandas, numpy |
| Data cleaning & validation | pandas |
| Exploratory analysis & statistical modeling | pandas (`groupby`, `corr`, `value_counts`) |
| Static visualizations (Week 2) | matplotlib, seaborn |
| Interactive BI dashboard (Week 3) | Microsoft Power BI, DAX |
| Executive Presentation | Microsoft PowerPoint (`AtmoSync.pptx`) |
| Version control | Git & GitHub |

---
## 🔮 Future Scope

* **Machine Learning Prediction:** Implement an XGBoost or Random Forest model to predict the exact hour a container will drop below the critical quality threshold based on early temperature drift.
* **Real-Time Data Streaming:** Transition from static CSV batches to a simulated real-time Kafka or AWS Kinesis stream to mimic live IoT sensor pings.
* **API Integration:** Connect with live market-pricing APIs to pull real-time commodity prices for dynamic arbitrage calculations.

## 📁 Repository Structure

```text
atmosync-analytics/
│
├── data/
│   ├── atmosync_dataset.csv              # Raw dataset (50,000 rows)
│   └── cleaned_dataset.csv               # Cleaned & validated dataset
│
├── notebooks/
│   ├── Dataset Cleaning.ipynb            # Initial cleaning & validation workflow
│   └── week2_dashboard_and_insights.ipynb# Visual dashboard & analysis generation
│
├── visuals/
│   ├── chart1_temperature_trace.png       # Continuous temperature monitoring trace
│   ├── chart2_temp_deviation_hist.png     # Distribution of temperature deviations
│   ├── chart3_quality_by_commodity.png    # Quality degradation per produce type
│   ├── chart4_quality_vs_transit_scatter.png # Transit duration vs. quality correlation
│   ├── chart5_risk_and_action_counts.png  # Risk severity vs. action counts
│   ├── chart6_correlation_heatmap.png     # Multi-metric feature correlation map
│   └── chart7_price_comparison.png        # Primary vs. secondary market prices
│
├── powerbi/
│   ├── AtmoSync_Dashboard.pbix           # Power BI dashboard file
│   └── PowerBI_ColdChain_Dashboard_Guide.md # Step-by-step build guide + DAX reference
│
├── AtmoSync.pptx                         # Stakeholder deck
└── README.md
```
