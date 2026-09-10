# Credit Card Customer Segmentation Using K-Means

## Overview

This project performs **customer segmentation on credit card usage data using K-Means clustering**. The analysis is implemented in the uploaded Jupyter Notebook, `Credit_card_using_K_Means.ipynb`, and uses `Credit_Card_Dataset.csv` as the input dataset.

The workflow covers data inspection, missing-value handling, feature scaling, selection of the number of clusters, K-Means clustering, PCA visualization, and cluster-level analysis.

## Dataset

The uploaded dataset contains:

- **Rows:** 8,950
- **Columns:** 18
- **Customer identifier:** `CUST_ID`
- **Modeling features:** 17

The dataset includes customer credit-card behavior such as:

- `BALANCE`
- `BALANCE_FREQUENCY`
- `PURCHASES`
- `ONEOFF_PURCHASES`
- `INSTALLMENTS_PURCHASES`
- `CASH_ADVANCE`
- `PURCHASES_FREQUENCY`
- `ONEOFF_PURCHASES_FREQUENCY`
- `PURCHASES_INSTALLMENTS_FREQUENCY`
- `CASH_ADVANCE_FREQUENCY`
- `CASH_ADVANCE_TRX`
- `PURCHASES_TRX`
- `CREDIT_LIMIT`
- `PAYMENTS`
- `MINIMUM_PAYMENTS`
- `PRC_FULL_PAYMENT`
- `TENURE`

### Missing values

The notebook identifies missing values in:

- `CREDIT_LIMIT`: 1
- `MINIMUM_PAYMENTS`: 313

The notebook replaces these missing values with the **median** of their respective columns before clustering.

## Project Workflow

### 1. Load and inspect the data

The notebook loads the CSV with pandas and examines:

- Dataset shape
- Data types and structure
- Descriptive statistics
- Missing values

### 2. Data preprocessing

A copy of the dataset is created. Missing values in `CREDIT_LIMIT` and `MINIMUM_PAYMENTS` are filled with their medians.

`CUST_ID` is removed from the modeling data because it is a customer identifier rather than a behavioral feature.

### 3. Feature scaling

The remaining features are standardized using `StandardScaler`.

This puts the variables on a comparable scale before applying K-Means.

### 4. Choose the number of clusters

The notebook evaluates different values of **K** using:

- **Elbow Method** — K values from 1 to 15
- **Silhouette Score** — K values from 2 to 10

The final notebook model uses:

```python
KMeans(n_clusters=4, random_state=42)
```

The reproduced silhouette results show that **K=2 has the highest silhouette score (approximately 0.280)** among the tested values, while the notebook proceeds with **K=4** for the final segmentation.

### 5. Apply K-Means clustering

The final K-Means model is fitted to the standardized customer features, and each customer is assigned a cluster label from **0 to 3**.

The resulting cluster sizes are:

| Cluster | Customers |
|---|---:|
| 0 | 977 |
| 1 | 1,487 |
| 2 | 3,118 |
| 3 | 3,368 |

### 6. PCA visualization

PCA is used to reduce the standardized feature set to two principal components. The notebook visualizes the customers before and after clustering to make the cluster structure easier to inspect.

### 7. Cluster profiling

The notebook calculates mean values for each cluster and visualizes selected variables, including:

- Average balance
- Average purchases
- Average credit limit
- Average cash advance
- Payments
- Percentage of full payment

A radar chart is also created to compare the cluster profiles.

## Cluster Profile

The mean values of several key variables in the final K=4 segmentation are:

| Cluster | Balance | Purchases | Cash Advance | Credit Limit | Payments | Full Payment % |
|---|---:|---:|---:|---:|---:|---:|
| 0 | 5010.39 | 716.02 | 5065.97 | 8208.65 | 4173.82 | 0.04 |
| 1 | 108.43 | 350.25 | 299.48 | 3632.11 | 1036.85 | 0.25 |
| 2 | 1253.82 | 2182.02 | 234.56 | 5121.99 | 2148.58 | 0.28 |
| 3 | 1495.32 | 283.48 | 782.29 | 3216.35 | 947.96 | 0.02 |

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
  - `StandardScaler`
  - `KMeans`
  - `silhouette_score`
  - `PCA`
- Jupyter Notebook / Google Colab

## Files

```text
.
├── Credit_card_using_K_Means.ipynb
├── Credit_Card_Dataset.csv
└── README.md
```

## How to Run

1. Place `Credit_card_using_K_Means.ipynb` and `Credit_Card_Dataset.csv` in the same project directory.
2. Open the notebook in Jupyter Notebook, JupyterLab, or VS Code.
3. Run the cells from top to bottom.

The notebook also contains a Google Colab upload step:

```python
from google.colab import files
Uploaded = files.upload()
```

If running locally, the CSV can instead be kept in the same directory as the notebook so that:

```python
pd.read_csv("Credit_Card_Dataset.csv")
```

can load it directly.

## Results and Interpretation

The K-Means analysis produces four customer groups with different average credit-card behavior. The notebook compares these groups using cluster-level averages and visualizations rather than assigning business names to the clusters.

For the K=4 solution:

- **Cluster 0** has the highest average balance and cash-advance activity among the four groups.
- **Cluster 1** has the lowest average balance and credit limit, with comparatively higher full-payment behavior.
- **Cluster 2** has the highest average purchases and a relatively high average credit limit.
- **Cluster 3** has moderate average balance and credit limit but comparatively low purchases and full-payment behavior.

These descriptions are based on the cluster averages generated from the uploaded dataset.

## Purpose

The project demonstrates an unsupervised-learning approach for discovering groups of customers with similar credit-card usage patterns. Such segmentation can be used as a starting point for further analysis of customer behavior, although the notebook itself does not perform downstream marketing or business-action recommendations.

## Author

Credit Card Customer Segmentation project using K-Means clustering.
