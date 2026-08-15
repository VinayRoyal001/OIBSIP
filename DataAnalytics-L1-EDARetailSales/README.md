# 🛍️ Retail Sales — Exploratory Data Analysis

> **Oasis Infobyte Internship · Data Analytics · Level 1 Task**

---

## 📌 Project Overview

Retail businesses generate large amounts of data through customer purchases, product sales, and daily transactions. Raw sales data alone does not directly explain customer behaviour or business performance.

In this project, **Exploratory Data Analysis (EDA)** is performed on a retail sales dataset to identify sales patterns, customer purchasing behaviour, popular products, and revenue trends. Statistical methods and data visualisations are used to transform raw data into meaningful business insights.

---

## 🎯 Objectives

The analysis helps the business understand:

| # | Question |
|---|----------|
| 1 | When sales are **highest or lowest** (monthly / quarterly trends) |
| 2 | Which **products and categories** generate the most revenue |
| 3 | Which **customer groups** purchase more frequently |
| 4 | Whether **age and gender** influence purchasing behaviour |
| 5 | Which factors are **associated with higher sales** |
| 6 | What **actions** can improve future business performance |

---

## 📂 Project Structure

```
DataAnalytics-L1-EDARetailSales/
├── retail_sales_eda.ipynb   ← Jupyter Notebook (interactive EDA)
├── retail_sales_eda.py      ← Python script (auto-saves all charts)
├── dataset/
│   └── retail_sales_dataset.csv
├── screenshots/             ← All output chart images (auto-generated)
├── requirements.txt
└── README.md
```

---

## 📊 Dataset Description

| Column | Type | Description |
|--------|------|-------------|
| Transaction ID | int | Unique transaction identifier |
| Date | date | Transaction date (2023-01-01 → 2024-01-01) |
| Customer ID | str | Unique customer identifier |
| Gender | str | Male / Female |
| Age | int | Customer age (18–64) |
| Product Category | str | Beauty / Clothing / Electronics |
| Quantity | int | Number of items purchased (1–4) |
| Price per Unit | int | Price per single item (₹) |
| Total Amount | int | Total transaction value (₹) |

**Shape:** 1 000 rows × 9 columns | **No missing values** | **No duplicates**

---

## 🔍 Analysis Sections

### 1 · Data Loading & Inspection
- Shape, data types, missing values, duplicate records
- Preview of first 5 rows

### 2 · Descriptive Statistics
- Mean, Median, Mode, Standard Deviation
- Full `describe()` summary for all numeric columns

### 3 · Time Series Analysis
- **Monthly Sales Trend** — line chart of revenue per month
- **Quarterly Sales Trend** — Q1–Q4 revenue comparison

### 4 · Customer & Product Analysis
- Sales breakdown by **Product Category**
- **Gender distribution** (pie chart + bar chart)
- **Customer Age distribution** with mean/median lines
- **Sales by Age Group** (18-25, 26-35, 36-45, 46-55, 56+)

### 5 · Purchase Behaviour
- Distribution of **Total Purchase Amount**
- **Quantity** purchased per transaction
- Category × Gender cross-analysis

### 6 · Correlation Analysis
- Heatmap of correlations between Age, Quantity, Price per Unit, Total Amount

### 7 · Price Analysis
- Average Price per Unit by Category
- Box plot of Price distribution per Category

---

## 💡 Key Insights

| Insight | Finding |
|---------|---------|
| 📅 Best Sales Month | **May 2023** — likely driven by seasonal demand |
| 📉 Lowest Sales Month | **September 2023** |
| 🏆 Top Category | **Electronics** — highest total revenue |
| 👥 Gender Split | Roughly equal — slight Female majority |
| 🎂 Avg Customer Age | ~41 years |
| 🛒 Most Common Qty | 4 items per transaction |
| 💰 Avg Transaction Value | ₹456 |

---

## 🚀 How to Run

### Jupyter Notebook (Recommended)
```bash
pip install -r requirements.txt
jupyter notebook retail_sales_eda.ipynb
```

### Python Script (auto-saves all charts)
```bash
pip install -r requirements.txt
python retail_sales_eda.py
```

All charts will be saved automatically to the `screenshots/` folder.

---

## 📸 Output Screenshots

All visualisation outputs are saved in the `screenshots/` folder:

| File | Description |
|------|-------------|
| `01_monthly_sales_trend.png` | Monthly revenue line chart |
| `02_quarterly_sales_trend.png` | Quarterly revenue line chart |
| `03_sales_by_category.png` | Revenue by product category |
| `04_gender_analysis.png` | Gender distribution + sales |
| `05_age_distribution.png` | Customer age histogram |
| `06_sales_by_age_group.png` | Revenue by age group |
| `07_total_amount_distribution.png` | Transaction value histogram |
| `08_quantity_distribution.png` | Quantity frequency bar chart |
| `09_sales_category_gender.png` | Category × Gender sales |
| `10_correlation_heatmap.png` | Numeric correlation heatmap |
| `11_price_analysis.png` | Price analysis by category |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, manipulation |
| `matplotlib` | Core plotting |
| `seaborn` | Statistical visualisations |
| `numpy` | Numerical computations |

---

## 👤 Author

**Vinay** · Oasis Infobyte Data Analytics Internship  
*Task: Level 1 — Exploratory Data Analysis on Retail Sales Data*
