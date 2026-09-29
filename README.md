# Customer Segmentation Using Clustering

A customer segmentation project using unsupervised machine learning techniques to identify groups of customers based on their purchasing behavior.

## Project Overview

This project applies clustering techniques to the **Online Retail** dataset.

The original dataset contains transaction-level records. Since the goal is customer segmentation, the transactions are transformed into **customer-level behavioral features** before applying clustering algorithms.

The main objective is to explore whether customers can be grouped into meaningful segments based on factors such as:

* Purchase frequency
* Revenue
* Quantity purchased
* Product variety
* Recency
* Purchase duration
* Cancellation behavior

---

## Dataset

The project uses the **Online Retail** dataset, which contains transactions from a UK-based online retail business.

The original dataset contains:

* **541,909 transactions**
* **8 original features**
* Transactions from **38 countries**
* Transaction dates ranging from **December 2010 to December 2011**

Main features include:

| Feature       | Description                  |
| ------------- | ---------------------------- |
| `InvoiceNo`   | Invoice number               |
| `StockCode`   | Product code                 |
| `Description` | Product description          |
| `Quantity`    | Number of products purchased |
| `InvoiceDate` | Transaction date             |
| `UnitPrice`   | Price per unit               |
| `CustomerID`  | Customer identifier          |
| `Country`     | Customer's country           |

A `Payment` feature was also created:

```text
Payment = Quantity × UnitPrice
```

---

## Problem Definition

The main question of the project is:

> **Can customers be grouped into distinct behavioral segments using their historical transaction data?**

Because there are no predefined customer labels, this is treated as an **unsupervised learning problem**.

---

## Data Exploration & Cleaning

The dataset was investigated before clustering to understand unusual transactions and data quality issues.

The analysis includes:

* Missing-value investigation
* Duplicate transaction detection
* Country distribution analysis
* Invoice number investigation
* Cancellation analysis
* Negative quantity investigation
* Zero-price transaction investigation
* Negative-price transaction investigation
* Analysis of unusual transaction descriptions

### Cancellation & negative transactions

The `InvoiceNo` field was investigated to understand different transaction types.

Transactions beginning with `C` were identified as cancellation transactions.

Negative-quantity transactions were also investigated separately because not all negative quantities represented exactly the same business event.

This step was important because these transactions can strongly affect customer-level behavioral features.

---

## Feature Engineering

Instead of clustering individual transactions, transaction records were aggregated at the **customer level**.

Several customer-level behavioral features were created, including:

### Purchase behavior

* Total number of invoices
* Total quantity purchased
* Total revenue
* Average revenue
* Number of different products purchased

### Temporal behavior

* Purchase duration
* Last purchase date
* Recency in days

### Cancellation behavior

* Number of cancellations
* Cancelled quantity
* Cancellation revenue
* Cancellation percentage

These features were combined into a customer-level dataset called:

```python
Customer_summary
```

---

## Clustering Methods

Two clustering algorithms were investigated.

### 1. K-Means

K-Means clustering was used to partition customers into different groups.

The number of clusters was investigated using the:

* Elbow Method
* Silhouette Score

The project evaluated values of `K` from 2 to 10.

Example:

```python
KMeans(
    n_clusters=k,
    random_state=42,
    n_init=10
)
```

---

### 2. Agglomerative Clustering

Hierarchical Agglomerative Clustering was also investigated using Ward linkage.

Different numbers of clusters were evaluated and their Silhouette Scores were compared.

```python
AgglomerativeClustering(
    n_clusters=k,
    linkage="ward"
)
```

---

## Cluster Evaluation

The **Silhouette Score** was used to evaluate the separation and cohesion of the generated clusters.

For the K-Means experiments, the project obtained the following example results:

| Number of Clusters | Silhouette Score |
| -----------------: | ---------------: |
|                  2 |           0.9876 |
|                  3 |           0.9574 |
|                  4 |           0.9516 |
|                  5 |           0.8024 |
|                  6 |           0.8025 |

The Elbow Method was also used to examine the relationship between the number of clusters and K-Means inertia.

> Note: The clustering results are dependent on the feature representation and preprocessing strategy used in the notebook.

---

## Visualization

Customer clusters were visualized using selected behavioral features, including:

* Purchase duration
* Revenue
* Cluster labels

This provides a visual representation of how customers are distributed across the generated groups.

---

## Technologies

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

Main machine learning techniques:

* K-Means Clustering
* Agglomerative Clustering
* Silhouette Analysis
* Elbow Method
* Feature Engineering
* Exploratory Data Analysis

---

## Project Structure

```text
Customer-Segmentation/
│
├── Customer_segmentation.ipynb
├── README.md
├── requirements.txt
│
└── data/
    └── Online Retail.xlsx
```

---

## Workflow

The overall workflow of the project is:

```text
Raw Transaction Data
        │
        ▼
Data Understanding
        │
        ▼
Data Cleaning
        │
        ▼
Transaction Analysis
        │
        ▼
Customer-Level Feature Engineering
        │
        ▼
Customer Feature Matrix
        │
        ├───────────────┐
        ▼               ▼
     K-Means      Agglomerative
        │               │
        ▼               ▼
 Elbow + Silhouette   Silhouette
        │               │
        └───────┬───────┘
                ▼
       Customer Clustering
```

---

## Key Learning Outcomes

Through this project, the following concepts were explored:

* Working with large transactional datasets
* Understanding messy real-world retail data
* Investigating unusual transaction patterns
* Customer-level feature engineering
* Unsupervised learning
* K-Means clustering
* Hierarchical clustering
* Elbow Method
* Silhouette Score
* Cluster visualization

---

## Future Improvements

Several improvements can make the clustering pipeline more robust:

* Apply feature scaling before distance-based clustering
* Compare different preprocessing strategies
* Investigate outliers before clustering
* Compare K-Means and Agglomerative clustering more systematically
* Perform deeper cluster profiling
* Analyze the behavioral characteristics of each customer segment
* Assign meaningful business interpretations to the resulting clusters
* Explore additional clustering algorithms such as DBSCAN or HDBSCAN

---

## Author

**Mohammad Mahdavimajd**

This project was developed as part of my practical exploration of **Data Science, Machine Learning, and Unsupervised Learning**.
