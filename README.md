# Australian-Retail-Customer-Segmentation

## Overview
This project segments 788 retail customers from a dataset (2018–2022) using RFM (Recency, Frequency, Monetary) analysis and K-means clustering. The goal is to identify customer segments for a business dashboard.

## Dataset
- **Source**: `dataaus.csv` (5,000 transactions, 789 unique customers)
- **Cleaned Version**: `dataausclean.csv`

## Methodology
1. **Data Cleaning**:
   - Removed `$` and `,` from financial columns, converted to floats.
   - Handled missing values (e.g., `address` with mode, `order_quantity($)` with mean).
2. **Transaction ID Assignment**:
   - Fixed 1,435 `order_no` (403 valid, 1,032 invalid) with `transaction_id` (e.g., `TX1000` to `TX4999`).
3. **Financial Recalculation**:
   - Recalculated `sub_total($)`, `discount_amount($)`, `order_total($)` using correct formulas.
   - Capped outliers (e.g., 15.96% in `profit_margin($)`).
4. **RFM Preparation**:
   - Recency: Days since last `order_date` (1,232–2,689 days from June 23, 2025).
   - Frequency: Unique `transaction_id` count (1–51).
   - Monetary: Sum of `order_total($)` (filtered out zero/negative).
5. **Normalization**:
   - Scaled RFM to mean ~0, std ~1 using `StandardScaler`.
6. **K-means Clustering**:
   - Segmented 788 customers into 3 clusters using elbow method.
   - Clusters: 414 (occasional), 106 (loyal high-value), 268 (churned).
7. **Visualization and Insights**:
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
