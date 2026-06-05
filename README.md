# Pricing Strategies & Influence on Sales

> *How much can price fluctuations affect sales — and which products are most sensitive?*


---

## Overview

This project uses real-world e-commerce behavioural data to investigate the relationship between price changes and sales volume. Using the top 10 best-selling products from a large anonymised dataset, we measure price–demand correlation and assess how consistently price reductions translate into higher sales.

**Data source:** [RetailRocket E-Commerce Dataset — Kaggle](https://www.kaggle.com/datasets/retailrocket/ecommercedataset?resource=download)

---

## Research Question

> How much do price fluctuations affect sales, and which products are the most affected?

---

## Dataset

Raw behavioural data collected from a real-world e-commerce platform. All values are hashed for confidentiality. The dataset consists of four files:

| File | Description |
|------|-------------|
| `events.csv` | User behaviour events (views, add-to-cart, transactions) |
| `item_properties_part1.csv` | Item attributes including prices |
| `item_properties_part2.csv` | Item attributes (continued) |
| `category_tree.csv` | Product category hierarchy |

- **Total sales events extracted:** 22,457
- **Products analysed:** Top 10 by quantity sold

---

## Methodology

### 1. Data Collection
Downloaded the three CSV files from Kaggle.

### 2. Data Cleaning & Filtering
- Filtered the events file to keep only `transaction` events
- Identified the top 10 most-sold products to keep the analysis tractable
- Retrieved each sale's price from the item properties files using the latest price recorded before the timestamp of the sale
- Removed rows where price data was unavailable

### 3. Analysis
- Computed month-to-month sales and price changes for each of the 10 products
- Calculated the Pearson correlation between price and quantity sold per product
- Computed a global correlation across all products combined
- Visualised price vs. sales trends and a per-product correlation heatmap

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3-blue?style=flat-square)
![pandas](https://img.shields.io/badge/pandas-data%20manipulation-150458?style=flat-square)
![matplotlib](https://img.shields.io/badge/matplotlib-visualisation-11557c?style=flat-square)
![seaborn](https://img.shields.io/badge/seaborn-heatmap-4c72b0?style=flat-square)

- **pandas** — data loading, filtering, merging, and aggregation
- **matplotlib** — price vs. sales trend line charts
- **seaborn** — per-product correlation heatmap
- **numpy** — numerical operations and NaN handling
- **re / os** — file handling and regex-based price extraction

---

## Results

### Global correlation

```
Overall correlation: -0.35
Range: -0.25 > r > -0.5  →  Weak negative relationship
```

### Per-product correlation (Price–Sales)

| Item ID | Correlation | Sensitivity |
|---------|-------------|-------------|
| 48030   | −1.00       | Very high   |
| 213834  | −0.98       | Very high   |
| 420960  | −0.98       | Very high   |
| 445351  | −0.97       | Very high   |
| 7943    | −0.78       | High        |
| 17478   | −0.64       | Moderate    |
| 312728  | −0.40       | Low         |
| 461686  | +0.33       | Inverse     |
| 119736  | +0.20       | Inverse     |
| 248455  | +1.00       | Strongly inverse |

### Key finding

Price changes do influence sales, but the effect varies significantly across products. The weak global correlation (−0.35) suggests that **price is not the only driver** — website traffic is identified as a likely additional variable explaining the remaining variance.

---

## Limitations

- **Hashed data** — product identifiers and attribute values are anonymised, making it impossible to interpret product categories or real price magnitudes
- **Short time horizon** — only 3–5 months of sales data, limiting detection of seasonal patterns or long-term trends
- **Missing variable** — the weak global correlation suggests that traffic volume likely mediates the price–sales relationship

---

## Future Work

The next logical step is a multivariate model examining how **traffic × price changes jointly explain sales volume** — moving from a bivariate correlation to a more realistic and predictive framework.

---

## References

- Dataset: [RetailRocket E-Commerce Dataset](https://www.kaggle.com/datasets/retailrocket/ecommercedataset)
- Reference notebook: [E-Commerce Recommendation using LFM](https://www.kaggle.com/code/faridsharaf/ecommerce-recommendation-using-lfm)
