# Australian-Retail-Customer-Segmentation

## Overview
This project segments 788 Australian retail customers (2018–2022) using RFM (Recency, Frequency, Monetary) analysis and K-Means clustering to optimize targeted marketing, retention, and customer lifetime value. A Power BI dashboard is in progress to visualize insights.

## Dataset
- **Source**: [Australia Retail Data](https://www.kaggle.com/datasets/chickenfulleton/australia-retail-data) (5,000 transactions, 788 unique customers)
- **Cleaned Version**: `dataausclean.csv`

## Tech Stack
Python (Pandas, NumPy, Matplotlib, Scikit-learn), Power BI, Jupyter Notebook

## Methodology
1. **Data Cleaning**:
   - Removed `$` and `,` from financial columns, converted to floats.
   - Handled missing values (e.g., `address` with mode, `order_quantity($)` with mean).
2. **Outlier Treatment**:
   - Detected outliers in 8 financial columns using IQR (e.g., 15.76% in `cost_price($)`).
   - Applied Winsorization to cap extreme values.
3. **Transaction ID Assignment**:
   - Corrected 1,032 invalid `order_no` values, assigned unique `transaction_id` (e.g., `TX1000` to `TX4999`).
4. **Financial Recalculation**:
   - Recalculated `sub_total($)`, `discount_amount($)`, `order_total($)` using correct formulas.
   - Capped outliers (e.g., 15.96% in `profit_margin($)`).
5. **RFM Analysis**:
   - Recency: Days since last `order_date` (1,232–2,689 days from June 23, 2025).
   - Frequency: Unique `transaction_id` count (1–51).
   - Monetary: Sum of `order_total($)` (excluded zero/negative values).
6. **Normalization**:
   - Scaled RFM metrics using `StandardScaler` (mean ~0, std ~1).
7. **K-Means Clustering**:
   - Identified 3 clusters via Elbow and Silhouette methods:
     - **Cluster 0 – Occasional Buyers**: Moderate recency, low frequency, low spend (n=414).
     - **Cluster 1 – Loyal High-Value Customers**: Recent, frequent, high spenders (n=106).
     - **Cluster 2 – Churned Customers**: Long inactive, low frequency, low spend (n=268).
8. **Visualization**:
   - 3D scatter plot (`rfm_3d_plot.png`) for RFM clusters.
   - Insights in `cluster_analysis.txt` and `cluster_insights.txt`.

## Files
- `dataaus.csv`: Original dataset
- `dataausclean.csv`: Cleaned dataset
- `rfm_data.csv`: RFM metrics
- `rfm_normalized.csv`: Normalized RFM
- `rfm_clustered.csv`: Clustered RFM
- `rfm_clustered_final.csv`: Final clustered data
- `powerbi_enriched_data.csv`: Data for Power BI
- `rfm_3d_plot.png`: 3D visualization
- `cluster_analysis.txt`: Cluster insights
- `cluster_insights.txt`: Detailed insights
- `powerbi_setup.txt`: Power BI setup guide
- `Retail_Segmentation.ipynb`: Main Jupyter Notebook

## Current Work
Building an interactive Power BI dashboard using `powerbi_enriched_data.csv` to visualize cluster sizes, RFM scatter plots, and customer type distributions.

## Next Steps
- Complete Power BI dashboard with live demo link.
- Update repository with dashboard screenshot and `.pbix` file.
