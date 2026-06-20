# Delivery Performance & Customer Satisfaction Analysis

Power BI dashboard analyzing the relationship between delivery timing and customer satisfaction in the Olist Brazilian e-commerce dataset (~99,000 orders).

## Overview

Most e-commerce dashboards built on this dataset default to a revenue-by-category, revenue-by-region view. This project deliberately moves away from that and asks a more specific operational question: **does late delivery actually affect customer satisfaction, and if so, where should attention be focused first?**

The dashboard was built end-to-end in Power BI, including data modeling across six relational tables, custom DAX measures, and statistical filtering to ensure category-level findings weren't driven by small-sample noise.

## Key Finding

Late delivery is rare, but its effect on customer satisfaction is severe.

| Metric | On-Time Orders | Late Orders |
|---|---|---|
| Share of orders | ~92% | ~8% |
| Average review score (out of 5) | 4.29 | 2.57 |

Only 8.1% of orders arrive after their estimated delivery date, yet that group's average review score drops by nearly two full points. This suggests delivery reliability initiatives should be evaluated by their effect on this tail of late orders, not by average delivery speed across the board.

## Dashboard Structure

The dashboard is organized in three layers:

1. **KPI row** — Average Order Value, Total Orders, Total Customers, % Late, Average Review Score
2. **Category & geographic breakdown** — late delivery rate by product category (filtered to a minimum order count to avoid small-sample distortion), and a scatter plot of late rate vs. order volume by state
3. **Trend & satisfaction link** — monthly trend of late delivery rate, a direct comparison of average review score for on-time vs. late orders, plus review score by category

## Data

**Source:** Olist Brazilian E-Commerce Public Dataset (Kaggle), covering orders placed between 2016 and 2018.

**Tables used:** `orders`, `order_items`, `products`, `product_category_name_translation`, `customers`, `order_reviews`

## Methodology Notes

- Category-level late-rate rankings exclude categories with fewer than 100 total orders, to avoid a handful of late orders producing a misleadingly high percentage in low-volume categories.
- The relationship between late delivery and review score is correlational. No causal test was run to separate delivery timing from other factors that could affect a review (e.g. product quality, pricing disputes).
- During development, a DAX `DATEDIFF`-based late-delivery measure returned an incorrect result (~11% instead of the verified ~8.1%) due to how the function evaluated the date comparison in this model. This was caught by independently verifying the percentage against the raw dataset in Python/pandas, and resolved by switching to direct date comparison logic in DAX.
- All final figures in this dashboard and the accompanying report are independently verified against the source data.

## Tools

- **Power BI Desktop** — data modeling, DAX, visualization
- **Python (pandas)** — independent verification of key metrics against raw source data

## Files

- `Delivery_Performance_Analysis_Report.pdf` — full written analysis report
- `dashboard_screenshot.png` — dashboard preview image

## Author

**Meerub Nadeem**
