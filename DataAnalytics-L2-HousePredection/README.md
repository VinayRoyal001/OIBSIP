# House Price Prediction

An end-to-end house price prediction project built for the **Oasis Infobyte (OIBSIP) Data Analytics Internship — Level 2**.

The project applies **Linear Regression**, **Ridge Regression**, and **Lasso Regression** with sklearn Pipelines to a synthetic house-price dataset to predict property prices based on structural and location features.

---

## 📁 Project Structure

```
DataAnalytics-L2-HousePredection/
├── House_Price_Prediction.ipynb   # Jupyter notebook with full walkthrough
├── Dataset/
│   └── house_prices.csv           # Raw house-price dataset (2,000 rows)
├── README.md                      # Project documentation (this file)
├── requirements.txt               # Python package dependencies
└── screenshots/
    ├── 01_price_distribution.png  # Histogram & box plot of target variable (Price)
    ├── 02_correlation_heatmap.png # Correlation heatmap of all features vs Price
    ├── 03_actual_vs_predicted.png # Scatter plot: Actual vs Predicted prices (Linear Regression)
    ├── 04_residual_plot.png       # Residual plot for the Linear Regression model
    ├── 05_residual_distribution.png  # Distribution of residuals
    └── 06_feature_coefficients.png   # Bar chart of Linear Regression coefficients
```

---

## 🗂️ Dataset

| Column | Type | Description |
|---|---|---|
| `Id` | Numeric | Unique row identifier |
| `Area` | Numeric | House area in sq ft (501 – 4,999) |
| `Bedrooms` | Numeric | Number of bedrooms (1 – 5) |
| `Bathrooms` | Numeric | Number of bathrooms (1 – 4) |
| `Floors` | Numeric | Number of floors (1 – 3) |
| `YearBuilt` | Numeric | Year the house was built (1900 – 2023) |
| `Location` | Categorical | Neighbourhood type (Downtown, Suburban, Urban, Rural) |
| `Condition` | Categorical | House condition (Excellent, Good, Fair, Poor) |
| `Garage` | Categorical | Garage availability (Yes / No) |
| `Price` | Target | House price in USD (50,005 – 999,656) |

- **Total records:** 2,000 rows
- **Missing values:** None
- **Duplicate rows:** None

---

## 🔍 Methodology

### 1. Dataset Loading & EDA
- Loaded the dataset with `pandas` and inspected shape, column names, data types, and number of records.
- Checked for missing values and duplicate rows — none found.
- Computed descriptive statistics for all numerical features.
- Visualised the target variable (`Price`) distribution with a histogram and box plot.
- Price skewness: **−0.06** (approximately normally distributed).

### 2. Correlation Analysis
- One-hot encoded categorical features (`Location`, `Condition`, `Garage`) before computing the correlation matrix.
- Plotted a heatmap of the correlation matrix.
- **Key finding:** All features showed very weak linear correlation with `Price` (max ~0.056 for `Floors`), indicating the dataset is synthetically generated with randomised prices.

### 3. Feature Engineering & Preprocessing Pipeline
Built separate sklearn `Pipeline` objects for numerical and categorical features:

| Step | Numerical | Categorical |
|---|---|---|
| Imputation | Median strategy | Most-frequent strategy |
| Encoding | — | One-Hot Encoding (`handle_unknown="ignore"`) |

Combined into a `ColumnTransformer` preprocessor.

**Features used:**
- Numerical: `Area`, `Bedrooms`, `Bathrooms`, `Floors`, `YearBuilt`
- Categorical: `Location`, `Condition`, `Garage`

### 4. Train-Test Split
- Split: **80% training / 20% testing** (`random_state=42`)
- Training set: 1,600 rows × 8 features
- Test set: 400 rows × 8 features

### 5. Model Training
Three regression models were trained inside full sklearn Pipelines (preprocessor + model):

| Model | Alpha |
|---|---|
| Linear Regression | — |
| Ridge Regression | 1.0 (default) |
| Lasso Regression | 1.0 (default) |

### 6. Model Evaluation

| Model | MSE | RMSE | R² Score |
|---|---|---|---|
| Linear Regression | 7.83 × 10¹⁰ | 279,859.5 | −0.0067 |
| Ridge Regression | Similar to Linear | Similar to Linear | Similar to Linear |
| Lasso Regression | Similar to Linear | Similar to Linear | Similar to Linear |

> **Note:** The near-zero (slightly negative) R² score is expected for this dataset. Because the prices were synthetically generated without a consistent relationship to the features, no linear model can learn meaningful patterns. This is reflected in all three models performing nearly identically.

### 7. Residual Analysis
- Plotted residuals (Actual Price − Predicted Price) against predicted prices.
- Plotted the distribution of residuals.
- Residuals showed a wide, near-uniform spread — confirming that the model is essentially predicting a constant (the mean price) for all houses.

### 8. Coefficient Analysis (Linear Regression)
Extracted and ranked feature coefficients by magnitude:

| Rank | Feature | Coefficient | Direction |
|---|---|---|---|
| 1 | Floors | +23,727 | Positive |
| 2 | Condition_Fair | +20,279 | Positive |
| 3 | Location_Suburban | +11,484 | Positive |
| 4 | Location_Rural | +1,290 | Positive |
| 5 | Garage_Yes | +1,187 | Positive |
| … | … | … | … |
| −3 | Bathrooms | −9,662 | Negative |
| −2 | Location_Urban | −12,747 | Negative |
| −1 | Condition_Good | −16,745 | Negative |

> Despite the low R² score, the coefficient directions are reasonable for a real dataset (e.g., more floors → higher price). The weak explanatory power is a consequence of the synthetic random pricing in the dataset.

---

## 📊 Visualisations

| Screenshot | Description |
|---|---|
| `01_price_distribution.png` | Histogram and box plot of house prices — shows near-normal distribution (skew ≈ −0.06) |
| `02_correlation_heatmap.png` | Heatmap showing correlation between all features and Price — all correlations very weak |
| `03_actual_vs_predicted.png` | Scatter plot of Actual vs Predicted prices — points scattered around a horizontal line at ~537K |
| `04_residual_plot.png` | Residual plot — wide uniform spread confirms model is predicting near the mean |
| `05_residual_distribution.png` | Distribution of residuals — approximately normal around zero |
| `06_feature_coefficients.png` | Horizontal bar chart of Linear Regression coefficients sorted by magnitude |

---

## ⚙️ Setup & Usage

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run the Jupyter Notebook

```bash
jupyter notebook House_Price_Prediction.ipynb
```

Run all cells in order for a step-by-step walkthrough with inline outputs and visualisations.

---

## 🛠️ Technologies Used

| Tool | Purpose |
|---|---|
| Python 3 | Core programming language |
| pandas | Data loading, cleaning, and transformation |
| scikit-learn | Pipelines, preprocessing, Linear/Ridge/Lasso Regression, evaluation metrics |
| matplotlib | Static plot generation |
| seaborn | Statistical visualisations (heatmaps, scatter plots, histograms) |
| numpy | Numerical operations (residual computation) |
| Jupyter Notebook | Interactive analysis environment |

---

## 📌 Key Findings

- The dataset contains **2,000 house records** with **no missing or duplicate values**.
- All features have **very weak linear correlation** with `Price` (max ≈ 0.056 for Floors), indicating the dataset is synthetically generated with prices that are **not strongly determined** by the provided features.
- All three models — **Linear Regression, Ridge, and Lasso** — produce nearly identical results (R² ≈ 0), which is expected given the randomised nature of the dataset.
- The **Floors** feature has the largest positive coefficient (+23,728), while **Condition_Good** has the largest negative coefficient (−16,745) in the Linear Regression model.
- The models effectively predict a value close to the **mean price (~$537,677)** for most houses, which is the best a linear model can do when there is no real signal in the features.

---

## 📄 License

This project is part of the **Oasis Infobyte (OIBSIP) Data Analytics Internship** programme.
