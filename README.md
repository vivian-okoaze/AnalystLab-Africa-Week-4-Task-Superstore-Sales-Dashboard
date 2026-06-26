# 📊 Superstore Sales Performance Dashboard
### Microsoft Power BI | Business Intelligence & Analytics Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Dataset](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Records](https://img.shields.io/badge/Records-9%2C994-blue?style=for-the-badge)
![Years](https://img.shields.io/badge/Years-2014--2017-purple?style=for-the-badge)

---

## 📌 Project Overview

This project presents a **two-page interactive business intelligence dashboard** built in Microsoft Power BI, analysing the Kaggle Superstore dataset. The dashboard transforms 9,994 rows of raw retail transaction data into clear, actionable business insights covering sales performance, regional profitability, customer segmentation, product analysis, and operational delivery efficiency.

The project was designed to answer real business questions that a retail executive or operations manager would ask — not just display numbers, but tell a story about where the business is winning, where it is losing, and what to do about it.

---

## 🗂️ Table of Contents

- [Project Overview](#-project-overview)
- [Dashboard Pages](#-dashboard-pages)
- [Dataset](#-dataset)
- [Key Performance Indicators](#-key-performance-indicators)
- [DAX Measures](#-dax-measures)
- [Key Insights](#-key-insights)
- [Recommendations](#-recommendations)
- [Tools & Technologies](#-tools--technologies)
- [Project Structure](#-project-structure)
- [How to Run](#-how-to-run)
- [Challenges & Solutions](#-challenges--solutions)
- [Author](#-author)

---

## 📺 Dashboard Pages

<img width="938" height="1059" alt="Presentation" src="https://github.com/user-attachments/assets/12a36097-cc1b-4d2c-9333-98fb39c0e797" />

### Page 1 — Sales Overview
> *Sales performance, regional breakdown, product profitability, and customer trends*

| Visual | Description |
|--------|-------------|
| 💳 KPI Cards | Total Sales, Total Profit, Profit Margin, Total Orders |
| 📊 Bar Chart | Total Sales by Region (West, East, Central, South) |
| 🍩 Donut Chart | Sales distribution by Category |
| 🗺️ Filled Map | Sales by US State (geographic heat map) |
| 📈 Line Chart | Monthly Sales Trend across 2014–2017 |
| 📋 Matrix Table | Sub-Category performance with conditional formatting (green = profit, red = loss) |

---

### Page 2 — Customer & Delivery Performance
> *Customer segmentation, top customers, shipping efficiency, and delivery analytics*

| Visual | Description |
|--------|-------------|
| 💳 KPI Cards | AOV, Total Customers, Total Quantity, Avg Delivery Days, Delayed Orders |
| 👥 Donut Chart | Sales by Customer Segment (Consumer, Corporate, Home Office) |
| 🏆 Bar Chart | Top 10 Customers by Revenue |
| 📦 Bar Chart | Orders by Ship Mode |
| ⏱️ Gauge Chart | On-Time Delivery Rate % |
| 📈 Line Chart | Average Delivery Days by Year and Quarter |
| 📊 Bar Chart | Most Profitable Products |

---

## 📁 Dataset

| Property | Detail |
|----------|--------|
| **Source** | [Kaggle — Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final) |
| **File** | `Sample - Superstore.csv` |
| **Rows** | 9,994 orders |
| **Columns** | 21 features |
| **Period** | January 2014 — December 2017 |
| **Geography** | United States (49 states) |
| **Missing Values** | None |

### Key Columns Used

| Column | Type | Purpose |
|--------|------|---------|
| Order Date | Date | Time intelligence, trend analysis |
| Ship Date | Date | Delivery performance calculation |
| Ship Mode | Text | Operational efficiency analysis |
| Segment | Text | Customer segmentation |
| Region / State | Text | Geographic performance |
| Category / Sub-Category | Text | Product analysis |
| Sales | Numeric | Revenue measure |
| Profit | Numeric | Profitability measure |
| Discount | Numeric | Discount impact analysis |
| Quantity | Numeric | Volume measure |
| Customer Name / ID | Text | Customer analytics |
| Order ID | Text | Unique order count |

---

## 📐 Key Performance Indicators

| KPI | Value | Insight |
|-----|-------|---------|
| Total Sales | $2.30M | Grew 51% from 2014 to 2017 |
| Total Profit | $286.4K | Thin but positive across 4 years |
| Profit Margin | 12.47% | Below 15% target — room to improve |
| Total Orders | 5,009 | Consistent order volume growth |
| Avg Order Value | $458.61 | Corporate segment drives highest AOV |
| Avg Delivery Days | 3.96 days | Acceptable but Q1 2018 spiked to 4.93 |
| On-Time Delivery Rate | 60% | Below 80% industry benchmark |
| Total Customers | 793 | Unique customers across all segments |

---

## 🧮 DAX Measures

### Sales & Profitability
```dax
Total Sales = SUM('Orders'[Sales])

Total Profit = SUM('Orders'[Profit])

Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)

Total Orders = DISTINCTCOUNT('Orders'[Order ID])

Avg Order Value = DIVIDE([Total Sales], [Total Orders], 0)

Total Quantity = SUM('Orders'[Quantity])

Sales % of Total = DIVIDE([Total Sales], CALCULATE([Total Sales], ALL('Orders')), 0)

Sales Growth% =
VAR Change = DIVIDE([Total Sales] - [Sales Last Year], [Sales Last Year], 0)
RETURN
IF(Change > 0, "▲ " & FORMAT(Change, "0.0%"), "▼ " & FORMAT(ABS(Change), "0.0%"))
```

### Delivery & Operations
```dax
-- Calculated Column & measures
Delivery Days = DATEDIFF('Orders'[Order Date], 'Orders'[Ship Date], DAY)

Avg Delivery Days = AVERAGE('Orders'[Delivery Days])

Delayed Orders = CALCULATE(COUNTROWS('Orders'), 'Orders'[Delivery Days] > 4)

On Time Rate = DIVIDE([On Time Orders], COUNTROWS('Orders'), 0)

```

### Year-over-Year Comparison
```dax
Sales LY = CALCULATE([Total Sales], DATEADD('Orders'[Order Date], -1, YEAR))


```

### Helper Columns (Power Query)
```m
Year = Date.Year([Order Date])
Month = Date.Month([Order Date])
Month Name = Date.MonthName([Order Date])
```

---

## 🔍 Key Insights

### 💰 Sales & Revenue
- Total revenue grew **51%** from $484K (2014) to $733K (2017)
- **November and December** consistently spike 35–40% above the monthly average every year — holiday season drives the business
- The overall profit margin of **12.47% is below the 15% target**, indicating over-discounting is eroding profitability

### 🌍 Regional Performance
- **West region** leads all regions with ~$725K revenue and the highest profit margin at 15.2%
- **Central region** is the hidden problem — third in sales but lowest margin at 7.8% due to excessive discounting
- **Texas** is the most urgent issue: top-5 state in sales volume but generates **-$25K in profit** — the business loses money on every Texas order

### 🛍️ Product Performance
- **Technology** is the star category: $836K revenue at 17.4% margin. Copiers deliver 37.2% margin — highest of all sub-categories
- **Tables (-8.56%)** and **Bookcases (-3.02%)** have been loss-making for 4 consecutive years — a structural problem, not an anomaly
- **Office Supplies** has hidden gems: Labels (44.42%), Paper (43.39%), and Envelopes (42.27%) are highly profitable but undermarketed

### 👤 Customer Segmentation
- **Consumer segment** dominates at 50.5% of total sales
- **Corporate segment** (30.74%) places larger individual orders — higher average order value per transaction
- **Sean Miller** is the single highest-value customer at $25K
- Top 10 customers represent a significant revenue concentration — retention is critical

### 🚚 Delivery & Operations
- **On-time delivery rate is only 60%** — well below the 80% industry benchmark. 4 in every 10 orders arrive late
- **Standard Class** carries 3,000+ orders (highest volume) but also the most delays
- **Q1 2018 spike to 4.93 days** is the worst delivery performance in the entire dataset — likely caused by holiday return overflow
- **Same Day shipping** is underutilised at only ~300 orders, suggesting low customer awareness or trust

---

## 💡 Recommendations

### 🔴 High Priority
| Action | Expected Impact |
|--------|----------------|
| Cap all discounts at 20% maximum | Recover estimated $80K+ annual profit |
| Conduct Texas market pricing review | Eliminate -$25K annual loss |
| Review or discontinue Tables & Bookcases | Stop 4-year structural losses |
| Investigate Q1 2018 delivery spike | Prevent recurrence in future Q1 periods |

### 🟡 Medium Priority
| Action | Expected Impact |
|--------|----------------|
| Increase Technology marketing budget | Grow highest-margin category |
| Bundle Office Supplies with larger orders | Unlock 40%+ margin hidden products |
| Build Q4 demand plan by October | Capture holiday spike without discounting |
| Improve Standard Class delivery SLA | Push on-time rate from 60% toward 80% |

### 🟢 Growth Opportunities
| Action | Expected Impact |
|--------|----------------|
| Launch VIP programme for top 10 customers | Protect high-value revenue concentration |
| Target Corporate segment for B2B growth | Higher AOV without new customer acquisition cost |
| Promote Same Day & First Class shipping | Increase revenue per order and reduce Standard Class pressure |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Microsoft Power BI Desktop** | Dashboard building, DAX measures, visualizations |
| **Power Query (M Language)** | Data cleaning, date type fixing, helper columns |
| **DAX (Data Analysis Expressions)** | KPI measures, time intelligence, conditional logic |
| **Kaggle** | Dataset source |
| **Microsoft Bing Maps** | Geographic map visualization |

---

## 📂 Project Structure

```
superstore-powerbi-dashboard/
│
├── 📊 Superstore_Dashboard.pbix          # Power BI project file
├── 📄 Sample - Superstore.csv            # Raw dataset (from Kaggle)
├── 📋 README.md                          # Project documentation
│
│   ├── page1_sales_overview.png          # Sales Overview dashboard screenshot
│   └── page2_delivery_performance.png   # Customer & Delivery dashboard screenshot
│
└── 📁 presentation/
    └── Superstore_Presentation.pptx      # Project presentation slides
```

---

## ▶️ How to Run

### Prerequisites
- Microsoft Power BI Desktop (free download at [powerbi.microsoft.com](https://powerbi.microsoft.com))
- The Superstore dataset CSV file from [Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)

### Steps

**1. Clone this repository**
```bash
git clone https://github.com/vivianokoaze/analystlab-africa-week-4-task-superstore-sales-dashboard
```

**2. Open the Power BI file**
- Double-click `Superstore_Dashboard.pbix`
- Power BI Desktop will open automatically

**3. Refresh the data source**
- Go to Home → Transform Data → Data Source Settings
- Update the file path to where you saved `Sample - Superstore.csv`
- Click Close & Apply

**4. Explore the dashboard**
- Use the page tabs at the bottom to switch between Page 1 and Page 2
- Use the Year, Category, and Region slicers to filter the data
- Click any chart to cross-filter all other visuals on the page
- Right-click any sub-category in the table → Drill through → Product Detail

---

## ⚠️ Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Order Date and Ship Date imported as Text type | Changed data type to Date in Power Query Editor |
| Avg Delivery Days created as a Column instead of Measure | Deleted column and recreated as a DAX Measure using `AVERAGE()` 
| Line chart x-axis too crowded with monthly labels | Removed combined date field and used Year only on X-axis with drill-down hierarchy |
| Growth indicator arrows not available in older Power BI version | Built arrow symbols directly into DAX measure using `IF` and `FORMAT` functions |

---

## 👩‍💻 Author

**Vivian Okoaze**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vivianokoaze)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/vivian-okoaze-108369173)

---

## 📄 License

This project is for educational purposes. The dataset is publicly available on Kaggle under the [CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/) license.

---

