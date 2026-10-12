# 🛒 Customer Retention & Segmentation Dashboard
![Python](https://img.shields.io/badge/Language-Python-blue)
![Power BI](https://img.shields.io/badge/Tool-Power%20BI-yellow)
![DAX](https://img.shields.io/badge/Language-DAX-blue)
![Analysis](https://img.shields.io/badge/Type-Customer%20Analytics-orange)
![Status](https://img.shields.io/badge/Status-Complete-success)

## 🎯 Project Overview
This project analyzes e-commerce transaction data spanning Jan 2024 to Dec 2025 to answer one business question: **which customers are valuable, which are leaving, and how can we keep them?** Using Python (Pandas) for data cleaning, RFM segmentation, and cohort analysis, and Power BI with DAX for a 3-page dashboard, the analysis shows where revenue is concentrated, which segment is at risk, and what action to take for each customer group.

---

## 📸 Dashboard Preview

### Page 1: Customer Value Overview
<img width="931" height="527" alt="Image" src="https://github.com/user-attachments/assets/3600e5ae-83f8-4e10-8ef2-024ecb490ca8" />

### Page 2: Segments and Retention
<img width="933" height="527" alt="Image" src="https://github.com/user-attachments/assets/001e2af7-916e-4927-9535-9408f12ff7b1" />

### Page 3: What Should We Do Next?
<img width="1064" height="597" alt="Image" src="https://github.com/user-attachments/assets/390719a8-4c67-4343-9543-31d986d364ae" />

---

## 📈 Key Metrics
| Metric | Value |
|--------|-------|
| **Total Revenue (completed orders)** | 1.88M |
| **Customers with 1+ completed order** | 2,047 (out of 3,600 signups) |
| **Completed Orders** | 8,456 |
| **Average Order Value** | ~222.57 |
| **Average Revenue per Customer** | ~919 |
| **Repeat Purchase Rate** | 64.39% |
| **Top 20% Customers' Revenue Share** | 62% |
| **Time Period** | Jan 2024 – Dec 2025 |
| **Customer Segments** | 5 (RFM-based) |

---

## 🔍 Key Findings

### 💡 Revenue Is Concentrated in a Few Customers
> **Top 20% of customers drive 62% of revenue, and 36% of customers drive 80%**

The top 10% alone contribute 44% of revenue. Losing even a small group of high-value customers has an outsized impact on the business.

### 🔁 Repeat Customers Carry the Business
> **64.39% of buyers purchased 2+ times and generate 92.2% of revenue**

One-time buyers (35.61%) contribute only 7.8% of revenue, so retention matters far more than one-off sales.

### ⚠️ At-Risk Customers Hold the Most Revenue
> **618 At-Risk customers hold 802.6K (42.6%) of revenue, with an average of 343 days since their last purchase**

These customers were once valuable (average 5.7 orders) but have gone quiet. This is the single largest pool of revenue at risk.

### 🚪 Many Signups Never Purchase
> **43.1% of signups (1,553 customers) never completed a single order**

Only 56.9% of signups became buyers, and just 235 customers (about 18% of repeat buyers) reached the Champions segment. The problem is both activation (first purchase) and retention (coming back).

### 📉 Retention Drops Fastest After the First Month
Cohort analysis shows the steepest fall in active customers between month 0 and month 1, then a slower decline. Month-1 retention for the first five monthly cohorts ranged from 36% to 70%.

---

## 🧩 Customer Segments (RFM)
| Segment | Rule | Customers | Revenue | Share | Avg Recency | Recommended Action |
|---------|------|-----------|---------|-------|-------------|--------------------|
| **At-Risk** | R ≤ 2, F ≥ 2 | 618 | 802.6K | 42.6% | 343 days | "We miss you" discount, quick contact |
| **Champions** | R = 4, F ≥ 3, M ≥ 3 | 235 | 475.1K | 25.2% | 20 days | Reward / loyalty offer |
| **Loyal** | R ≥ 3, F ≥ 2 (not Champions) | 465 | 456.8K | 24.3% | 64 days | Upsell, early access |
| **Lost** | R ≤ 2, F = 1 | 403 | 80.6K | 4.3% | 344 days | Cheap win-back or ignore |
| **New** | R ≥ 3, F = 1 | 326 | 67.0K | 3.6% | 51 days | Nudge for a second order |

---

## 💼 Business Recommendations
Based on the analysis, the following actions are recommended:

1. **Win Back At-Risk Customers First**
   They hold 42.6% of revenue. Prioritize quick, personal outreach and a targeted "We miss you" offer instead of sending the same discount to everyone.

2. **Protect Champions**
   235 customers generate 25.2% of revenue. Reward them with loyalty offers before they become At-Risk.

3. **Grow Loyal Customers into Champions**
   The Loyal segment is large (465 customers, 24.3% of revenue). Upselling and early access can lift their frequency and spend.

4. **Fix the Activation Gap**
   43.1% of signups never bought. A first-purchase offer or onboarding email could convert part of this group.

5. **Improve First-Month Retention**
   Since the biggest drop happens after month 0, nudge new buyers toward a second order within their first month.

---

## 🛠️ Technical Approach

### Python & Analysis:
- **Data Cleaning**: Validated data types and duplicates, removed duplicate order records, and filled 199 missing `unit_price` values using the product-wise mode
- **Revenue Definition**: `quantity × unit_price − discount_amount`; shipping fees excluded; only `completed` orders counted
- **Revenue Concentration**: Ranked customers by revenue to measure top 10%, 20%, and 50% shares and the share of customers needed for 80% of revenue
- **RFM Segmentation**: Recency (days since last order, snapshot = last order date + 1 day), Frequency (unique orders), and Monetary (total revenue); scored 1–4 using quartiles for R and M and custom bins for F (1 | 2 | 3–4 | 5+)
- **Cohort Analysis**: Grouped customers by first-purchase month and tracked active customers by months since first purchase

### Power BI & DAX Techniques Used:
- **Core Measures**: `DISTINCTCOUNT` for customers and orders, `DIVIDE` for safe percentage calculations
- **Filter Context**: `CALCULATE` with `ALL` for segment share of total revenue and repeat customer counts
- **Top-N Analysis**: `VAR`, `TOPN`, and `SUMX` for the top 20% revenue share
- **Heatmap & Curves**: Matrix with conditional formatting for cohort retention, line chart for the average retention curve
- **Interactive Dashboard Design**: 3 pages with slicers, a consistent colour palette, and clear segment colours

---

## 📊 Data Model

### Source Tables (raw CSV):
**`customers`**: `customer_id`, `signup_date`, `state`, `acquisition_channel`
**`orders`**: `order_id`, `customer_id`, `order_date`, `status`, `payment_method`, `discount_code`, `shipping_fee`
**`order_items`**: `order_id`, `product_id`, `quantity`, `unit_price`, `discount_amount`
**`products`**: `product_id`, `product_name`, `category`, `list_price`, `unit_cost`

### Power BI Tables (built in Python):
**`pbi_customers`**: one row per customer with `total_revenue`, `num_orders`, `first_order`, `last_order`, `recency_days`, R/F/M scores, `segment`, and `cohort_month`
**`pbi_sales`**: order-item level data for completed orders with `line_revenue` and product category
**`pbi_cohort_retention`**: `cohort_month`, `months_since_first`, `retention_pct`
**`pbi_concentration`**: `customer_pct`, `revenue_pct` (for the concentration curve)

---

## 📁 Project Structure
```
customer-retention-analysis/
├── data/
│   ├── raw/                  # original 4 CSV files
│   └── processed/            # cleaned and Power BI-ready tables
├── notebooks/
│   ├── 01_data_understanding_cleaning.ipynb
│   ├── 02_revenue_concentration_repeat_rate.ipynb
│   ├── 03_rfm_segmentation.ipynb
│   └── 04_cohort_retention.ipynb
├── dashboard/                
└── README.md
```

---

## ⚠️ Limitations
- **Revenue, not profit**: product cost and shipping fees are not included, so segment value reflects sales, not margin
- **Completed orders only**: canceled and returned orders are excluded from revenue, RFM, and cohort analysis
- **Imputed prices**: 199 missing `unit_price` values (~1.3% of item rows) were filled with the product-wise mode; filled values can differ from the true price by up to ~5%
- **Historical, not predictive**: At-Risk is defined by past behavior; it shows who stopped buying, not who will definitely return
- **Observation window**: recent customers have had little time to repeat, so repeat rate and recent-cohort retention are understated, and late-month retention percentages rest on very few customers
- **Rule-based segments**: segment thresholds are analyst judgment, so different cut-offs would move customers between segments
- **No causal claims**: the recommended actions are not tested; an A/B test would be needed to measure their impact

---

## 📧 Contact
For questions or collaboration opportunities, feel free to reach out!
- 🔗 [LinkedIn Profile](https://www.linkedin.com/in/izaan-ansari/)
- 💻 [GitHub Profile](https://github.com/iza684)
- 📧 [Email](izaanansari2408@gmail.com)

---

⭐ **If you found this project useful, please consider giving it a star!**
