# Customer Segmentation Analysis

An end-to-end customer segmentation project built for the **Oasis Infobyte (OIBSIP) Data Analytics Internship — Level 1**.

The project applies **RFM (Recency, Frequency, Monetary) analysis** and **K-Means clustering** to an e-commerce dataset to identify distinct customer segments and recommend targeted marketing actions for each group.

---

## 📁 Project Structure

```
DataAnalytics-L1-Customer Segmentation Analysis/
├── customer_segmentation_analysis.ipynb   # Jupyter notebook with full walkthrough
├── customer_segmentation_analysis.py      # Standalone Python script
├── dataset.csv                            # Raw e-commerce dataset (root copy)
├── customer_segments.csv                  # RFM data with cluster labels per customer
├── cluster_profile.csv                    # Mean RFM values and customer type per cluster
├── README.md                              # Project documentation (this file)
├── requirements.txt                       # Python package dependencies
└── screenshots/
    ├── 01_data_preview.png                # First 5 rows of the cleaned dataset
    ├── 02_rfm_analysis.png                # Recency vs Monetary scatter coloured by cluster
    ├── 03_elbow_method.png                # Elbow curve used to select K=4
    ├── 04_customer_clusters.png           # Scatter plot with customer-type labels
    └── 05_cluster_distribution.png        # Bar chart of customer counts per cluster
```

The `dataset/` folder contains:
- `ecommerce_dataset_updated.csv` — original dataset used for analysis
- `customer_segment_marketing_insights.csv` — marketing recommendations exported by the notebook

---

## 🗂️ Dataset

| Column | Description |
|---|---|
| `User_ID` | Unique identifier for each customer |
| `Product_ID` | Unique identifier for each product |
| `Category` | Product category (e.g. Sports, Clothing, Books) |
| `Price (Rs.)` | Original product price in Indian Rupees |
| `Discount (%)` | Discount percentage applied |
| `Final_Price(Rs.)` | Price paid after discount |
| `Payment_Method` | Payment method used (UPI, Credit Card, Net Banking) |
| `Purchase_Date` | Date of the purchase transaction |

- **Total records:** ~3,660 rows (before deduplication)
- **Unique customers (after cleaning):** 1,454

---

## 🔍 Methodology

### 1. Data Loading & Cleaning
- Loaded the dataset with `pandas`, parsed `Purchase_Date` as datetime, and cast `Final_Price` to numeric.
- Removed rows with missing values in key columns (`User_ID`, `Product_ID`, `Purchase_Date`, `Final_Price`).
- Dropped duplicate records.

### 2. Descriptive Statistics
Computed per-customer statistics:
- **Average Purchase Value** — mean spend per transaction
- **Purchase Frequency** — total number of purchases
- **Total Spending** — sum of all purchases
- **Estimated Customer Lifetime Value (CLV)** — Average Purchase Value × Purchase Frequency

### 3. RFM Feature Engineering
Constructed three behavioural features per customer:

| Feature | Definition |
|---|---|
| **Recency** | Days since the customer's most recent purchase (relative to reference date = max date + 1 day) |
| **Frequency** | Total number of purchases made |
| **Monetary** | Total amount spent |

### 4. Standardisation
Applied `StandardScaler` to bring all three RFM features to a common scale (mean ≈ 0, std ≈ 1), ensuring no single feature dominates the clustering.

### 5. Elbow Method
Ran K-Means for K = 1 to 10 and plotted inertia values. The elbow appeared at **K = 4**, which was selected as the optimal number of clusters.

### 6. K-Means Clustering (K = 4)
Fitted K-Means with `n_clusters=4` and `random_state=42`. Each customer was assigned to one of four clusters.

### 7. Cluster Profiling & Customer Type Labelling
Computed mean RFM values per cluster and labelled each cluster with a descriptive customer type based on relative thresholds:

| Cluster | Customer Type | Mean Recency | Mean Monetary | Count |
|---|---|---|---|---|
| 0 | Loyal Customers | 77 days | Rs. 107 | 404 |
| 1 | At-Risk High-Value Customers | 270 days | Rs. 322 | 311 |
| 2 | Regular Customers | 264 days | Rs. 114 | 371 |
| 3 | Champions | 85 days | Rs. 317 | 368 |

---

## 📊 Visualisations

| Screenshot | Description |
|---|---|
| `01_data_preview.png` | Table showing the first 5 rows of the cleaned dataset |
| `02_rfm_analysis.png` | Scatter plot of Recency vs Monetary coloured by cluster number |
| `03_elbow_method.png` | Elbow curve showing inertia vs K (optimal K = 4) |
| `04_customer_clusters.png` | Scatter plot of Recency vs Monetary with customer-type labels |
| `05_cluster_distribution.png` | Bar chart comparing customer counts across all four clusters |

---

## 🎯 Marketing Recommendations

| Customer Type | Recommended Action |
|---|---|
| **Champions** | Provide VIP rewards, exclusive discounts, early product access and referral incentives. |
| **Loyal Customers** | Offer loyalty points, membership benefits, personalised recommendations and cross-selling offers. |
| **Regular Customers** | Promote product bundles, seasonal campaigns and incentives that encourage more frequent purchases. |
| **At-Risk High-Value Customers** | Launch personalised win-back campaigns, limited-time offers and recommendations based on previous purchases. |

---

## ⚙️ Setup & Usage

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run the standalone script

```bash
python customer_segmentation_analysis.py
```

This will:
- Load and clean the dataset
- Compute RFM features
- Run the Elbow Method and K-Means clustering
- Save `customer_segments.csv` and `cluster_profile.csv`
- Generate and save all five screenshots into the `screenshots/` folder
- Print a full analysis summary to the console

### 3. Run the Jupyter Notebook

```bash
jupyter notebook customer_segmentation_analysis.ipynb
```

Run all cells in order for a step-by-step walkthrough with inline outputs and visualisations.

---

## 🛠️ Technologies Used

| Tool | Purpose |
|---|---|
| Python 3 | Core programming language |
| pandas | Data loading, cleaning, and transformation |
| scikit-learn | StandardScaler and KMeans clustering |
| matplotlib | Static plot generation and figure saving |
| seaborn | Statistical visualisations (scatter plots, bar charts) |
| Jupyter Notebook | Interactive analysis environment |

---

## 📌 Key Findings

- The dataset contains **1,454 unique customers**, each making exactly **one purchase**.
- The **Champions** segment (Cluster 3) represents high-value, recently active customers — the most valuable group for retention.
- The **At-Risk High-Value Customers** (Cluster 1) spent significantly (mean Rs. 322) but haven't purchased in ~270 days — prime candidates for win-back campaigns.
- The **Loyal Customers** segment (Cluster 0, largest group at 404) purchased recently but with lower spend — cross-selling and upselling opportunities.
- The **Regular Customers** (Cluster 2) are lapsed low-spenders — seasonal promotions and bundles may re-engage them.

---

## 📄 License

This project is part of the **Oasis Infobyte (OIBSIP) Data Analytics Internship** programme.
