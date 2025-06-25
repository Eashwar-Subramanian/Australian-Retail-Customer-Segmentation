# Australian-Retail-Customer-Segmentation

## Overview
This project segments 788 retail customers after filtering (2018–2022) using RFM (Recency, Frequency, Monetary) analysis and K-Means clustering. The goal is to support targeted marketing, retention, and customer lifetime value insights through a Power BI dashboard.

## Dataset
- **Source**: `dataaus.csv` (5,000 transactions, 788 unique customers)
- **Cleaned Version**: `dataausclean.csv`

## Tech Stack: 
Python (pandas, numpy, matplotlib, sklearn), Power BI, Jupyter Notebook

## Methodology
1. **Data Cleaning**:
   - Removed `$` and `,` from financial columns, converted to floats.
   - Handled missing values (e.g., `address` with mode, `order_quantity($)` with mean).
2. **Outlier Detection & Treatment**:
   - Detected outliers in 8 financial columns using IQR (e.g., 15.76% in cost_price($)).
   - Applied Winsorization to cap extreme values, preserving statistical stability.
3. **Transaction ID Assignment**:
   - Fixed 1,435 `order_no` (403 valid, 1,032 invalid) with `transaction_id` (e.g., `TX1000` to `TX4999`).
4. **Financial Recalculation**:
   - Recalculated `sub_total($)`, `discount_amount($)`, `order_total($)` using correct formulas.
   - Capped outliers (e.g., 15.96% in `profit_margin($)`).
5. **RFM Preparation**:
   - Recency: Days since last `order_date` (1,232–2,689 days from June 23, 2025).
   - Frequency: Unique `transaction_id` count (1–51).
   - Monetary: Sum of `order_total($)` (Excluded customers with zero or negative monetary values from clustering.).
6. **Normalization**:
   - Scaled RFM to mean ~0, std ~1 using `StandardScaler`.
7. **K-means Clustering**:
   - Segmented 788 customers into 3 clusters using elbow method.
   - Cluster Profiles:
      - Cluster 0 – Occasional Buyers: Moderate recency, low frequency, low spend (n = 414).
      - Cluster 1 – Loyal High-Value Customers: Recent, frequent, high spenders (n = 106).
      - Cluster 2 – Churned Customers: Long inactive, low frequency, low spend (n = 268).
8. **Visualization and Insights**:
   - 3D scatter plot (`rfm_3d_plot.png`).
   - Summaries in `cluster_analysis.txt` and `cluster_insights.txt`.

## Files
- `dataaus.csv`: Original dataset.
- `dataausclean.csv`: Cleaned dataset.
- `rfm_data.csv`: RFM metrics.
- `rfm_normalized.csv`: Normalized RFM.
- `rfm_clustered.csv`: Clustered RFM.
- `rfm_clustered_final.csv`: Final clustered data.
- `powerbi_enriched_data.csv`: Data for Power BI.
- `rfm_3d_plot.png`: 3D visualization.
- `cluster_analysis.txt`: Initial cluster insights.
- `cluster_insights.txt`: Expanded insights.
- `powerbi_setup.txt`: Power BI setup guide.
- `Retail_Segmentation.ipynb`: Jupyter Notebook with all code and documentation.

## Current Work
I am currently working on visualizing and presenting the customer segments through a Power BI dashboard, using `powerbi_enriched_data.csv` to create interactive visuals (e.g., cluster sizes, recency vs. monetary scatter).
