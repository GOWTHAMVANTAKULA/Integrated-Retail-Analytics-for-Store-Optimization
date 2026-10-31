# Integrated-Retail-Analytics-for-Store-Optimization
An end-to-end retail analytics pipeline using machine learning. Features anomaly detection, K-Means store segmentation, market basket analysis, and XGBoost demand forecasting. Transforms historical sales and economic data into actionable strategies for inventory optimization and personalized marketing.

# 🏬 Integrated Retail Analytics for Store Optimization and Demand Forecasting

## 📌 Project Overview

This project focuses on analyzing historical Walmart sales data from **45 stores** to improve retail decision-making through data analytics and machine learning.

The objective is to identify unusual sales patterns, segment stores based on their characteristics, forecast future weekly sales, and develop targeted inventory and marketing strategies.

By combining exploratory data analysis, statistical techniques, and machine learning models, this project transforms historical retail data into actionable business insights.

## 🎯 Business Objectives

- **Anomaly Detection:** Identify unusual sales patterns across stores and departments and investigate possible causes such as holidays, markdowns, and economic changes.
- **Store Segmentation:** Group stores based on sales performance, store size, and regional economic indicators.
- **Demand Forecasting:** Predict future weekly sales for individual stores and departments.
- **Department Association Analysis:** Identify relationships between department-level sales patterns to support cross-selling opportunities.
- **Business Strategy:** Develop store-specific inventory management and promotional strategies based on sales patterns and store segments.

## 📂 Dataset Description

The project uses three datasets:

| Dataset | Description |
|---|---|
| Sales | Historical weekly sales records for stores and departments |
| Stores | Store information, including store type and size |
| Features | External factors such as temperature, fuel price, CPI, unemployment, holidays, and markdowns |

The datasets were merged to create a unified dataset for analysis and model development.

## 🛠️ Technologies & Libraries

| Category | Tools |
|---|---|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Machine Learning | Scikit-learn, XGBoost |
| Clustering | K-Means |
| Dimensionality Reduction | PCA |
| Data Preprocessing | StandardScaler |
| Visualization | Matplotlib, Seaborn |
| Statistical Analysis | Statsmodels |
| Anomaly Detection | IQR Method |
| Forecasting | Linear Regression, XGBoost Regressor |

## 🔄 Project Workflow

### 1. Data Preprocessing & Feature Engineering

- Loaded and merged the Sales, Stores, and Features datasets.
- Handled missing values in markdown columns by filling structural missing values with zero.
- Processed date columns and extracted temporal features such as Year, Month, and Week.
- Incorporated economic indicators and holiday information.
- Created a 4-week rolling average feature to capture recent sales trends.

### 2. Anomaly Detection

Applied the **Interquartile Range (IQR)** method to identify unusual weekly sales observations.

**Results:**
- Identified 35,521 potential outliers.
- Approximately 8.4% of observations were flagged.
- Retained the identified observations instead of automatically deleting them because unusual sales can represent genuine holiday demand and promotional activity.

**Business Insight:**

Unusual sales patterns can provide valuable information about seasonal demand, promotional effectiveness, and unexpected changes in customer purchasing behaviour.

### 3. Store Segmentation Using K-Means

Applied K-Means clustering to group stores based on aggregated sales performance, store size, and economic characteristics.

**Methodology:**
- Aggregated relevant features at the store level.
- Standardized numerical features using StandardScaler.
- Applied K-Means clustering.
- Used PCA to reduce dimensionality and visualize store clusters in two dimensions.

**Results:**

- Number of stores: 45
- Number of clusters: 3
- Silhouette Score: 0.3345
- Inertia: 107.18

**Business Insight:**

The clustering results help identify stores with different business characteristics, supporting more targeted inventory and promotional decisions.

### 4. Department Association Analysis

Developed a department-level co-occurrence and correlation heatmap to explore relationships between department sales patterns.

**Key Observation:**

Certain departments, including departments 87–99, showed interesting relationships in their sales patterns.

**Business Application:**

These relationships can help identify potential cross-selling opportunities and support coordinated promotional strategies.

*Note: Since individual customer transaction-level basket data was unavailable, this analysis represents department-level associations rather than traditional transaction-level Market Basket Analysis.*

### 5. Demand Forecasting

Developed regression models to predict weekly sales using historical sales information, store characteristics, holiday indicators, markdowns, and economic features.

**Models Implemented:**

1. Linear Regression – Baseline model.
2. XGBoost Regressor – Advanced tree-based regression model.

**Training and Testing Strategy:**

- Training data: 2010–2011
- Testing data: 2012
- Used chronological splitting to simulate forecasting on future periods.

**XGBoost Model Results:**

| Evaluation Metric | Result |
|---|---:|
| R² Score | 0.98 |
| Mean Absolute Error (MAE) | 1,351.54 |

**Feature Importance:**

The model identified the following important predictors:

- 4-week rolling average
- MarkDown3
- IsHoliday
- Month

**Business Insight:**

Recent sales trends, promotional activity, and seasonal patterns provide useful information for predicting weekly retail demand.

**Important Production Consideration – Target Leakage:**

The initial rolling average feature included current-week sales, which introduces target leakage when predicting that same week's sales.

For genuine future forecasting, the rolling average must be shifted by one week so that it uses only previously available sales data. Model performance should then be reevaluated using this corrected feature.

### 6. Store-Specific Marketing & Inventory Strategies

Developed a strategy matrix connecting store clusters with promotional and inventory decisions.

| Store Segment | Promotional Strategy | Inventory Strategy |
|---|---|---|
| High-volume stores (Cluster 1) | Premium and broader promotional campaigns using suitable markdowns | Maintain higher stock levels for consistently high-demand products |
| Low-volume stores (Cluster 2) | Targeted, price-sensitive promotions on essential products | Maintain controlled inventory to reduce excess stock |
| Other stores (Cluster 0) | Balanced promotions based on sales trends | Adjust stock levels according to historical demand |

These recommendations provide a starting point for store-specific business planning and should be validated against actual promotional performance and inventory data.

## 📈 Key Project Outcomes

- Integrated three datasets into a unified retail analytics dataset.
- Identified 35,521 potential sales anomalies using the IQR method.
- Segmented 45 Walmart stores into three clusters using K-Means.
- Achieved a Silhouette Score of 0.3345 for store segmentation.
- Built and evaluated Linear Regression and XGBoost regression models.
- Achieved an initial XGBoost R² score of 0.98 and MAE of 1,351.54.
- Identified important sales predictors and developed cluster-based marketing and inventory recommendations.

## ⚠️ Challenges & Limitations

**1. Missing Data**

Some markdown values were missing. These were handled based on the assumption that the missing values represented no markdown activity.

**2. Sales Anomalies**

Potential outliers were retained because they may represent genuine seasonal or promotional demand rather than data errors.

**3. Target Leakage**

The initial rolling average included current-week sales. A lagged rolling average is necessary for reliable future forecasting.

**4. Limited Customer-Level Information**

The dataset does not contain individual customer transaction records. Therefore, traditional customer segmentation and transaction-level market basket analysis cannot be performed directly.

**5. Forecasting Limitations**

External factors, unexpected demand changes, and supply chain constraints may affect actual sales beyond what historical data can predict.

## 🚀 Future Improvements

- Implement lagged rolling averages and additional lag features.
- Optimize XGBoost hyperparameters using cross-validation suitable for time-series data.
- Compare additional forecasting approaches.
- Evaluate forecasting performance separately for different stores and departments.
- Explore customer-level segmentation when transaction-level data becomes available.
- Develop an interactive Power BI dashboard for business users.
- Deploy the forecasting model through a REST API.

## 📁 Suggested Project Structure

```text
Integrated-Retail-Analytics/
│
├── data/
│   ├── sales.csv
│   ├── stores.csv
│   └── features.csv
│
├── notebooks/
│   ├── 01_Data_Preprocessing_EDA.ipynb
│   ├── 02_Anomaly_Detection.ipynb
│   ├── 03_Store_Segmentation.ipynb
│   ├── 04_Department_Association_Analysis.ipynb
│   └── 05_Demand_Forecasting.ipynb
│
├── models/
│   └── xgboost_model.pkl
│
├── visualizations/
│
├── README.md
└── requirements.txt
```

*The structure above is a suggested organization for the project.*

## 💡 Business Value

This project demonstrates how retail businesses can use historical sales data and machine learning to:

- Improve demand planning and inventory allocation.
- Identify unusual sales patterns.
- Understand differences in store performance.
- Support data-driven promotional strategies.
- Reduce the risk of overstocking and stockouts.
- Improve retail operational efficiency.

