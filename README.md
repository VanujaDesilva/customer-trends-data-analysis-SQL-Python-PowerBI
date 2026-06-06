# Customer Trends Data Analysis

A company-level retail analytics project that takes raw shopping transactions through a complete data pipeline: cleaning in Python, structured SQL analysis in PostgreSQL, and a published interactive Power BI dashboard with business KPIs.

---

## Project Summary

| Detail | Info |
|---|---|
| Dataset | 3,900 purchase records, 18 features |
| Tools | Python, PostgreSQL, Power BI |
| Libraries | pandas |
| Avg. Purchase Value | $59.76 |
| Avg. Review Rating | 3.75 / 5 |

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Python: Data Cleaning and EDA](#python-data-cleaning-and-eda)
- [SQL: Business Analysis](#sql-business-analysis)
- [Power BI Dashboard](#power-bi-dashboard)
- [Key Findings](#key-findings)
- [Business Recommendations](#business-recommendations)
- [How to Run](#how-to-run)
- [Project Structure](#project-structure)

---

## Project Overview

This project simulates a real-world retail analytics workflow. Starting from a raw CSV of shopping transactions, it covers every stage a data analyst would handle:

1. Load and clean the data in Python using pandas
2. Engineer new features and push the cleaned data to PostgreSQL
3. Run structured SQL queries to answer specific business questions
4. Visualize findings in an interactive Power BI dashboard

The goal is to help business stakeholders understand who their customers are, what they buy, and where the biggest growth opportunities lie.

---

## Dataset

The dataset contains **3,900 rows** and **18 columns** covering:

- **Customer demographics:** Age, Gender, Location, Subscription Status
- **Purchase details:** Item Purchased, Category, Purchase Amount (USD), Season, Size, Color
- **Shopping behavior:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type

**Missing data:** 37 null values in the `Review Rating` column, handled during cleaning.

---

## Python: Data Cleaning and EDA

**File:** `analysis.ipynb` or `analysis.py`

Steps performed:

1. **Data loading** using `pandas.read_csv()`
2. **Initial exploration** with `df.info()` and `df.describe()` to understand structure and distributions
3. **Missing data handling** — imputed the 37 missing `Review Rating` values using the median rating per product category
4. **Column standardization** — renamed all columns to `snake_case` for consistency
5. **Feature engineering:**
   - Created `age_group` by binning the `Age` column into meaningful ranges
   - Created `purchase_frequency_days` from the frequency of purchases field
6. **Redundancy check** — verified that `discount_applied` and `promo_code_used` were near-identical; dropped `promo_code_used`
7. **Database export** — connected to PostgreSQL via `psycopg2` / `SQLAlchemy` and loaded the cleaned DataFrame for SQL analysis

---

## SQL: Business Analysis

**Database:** PostgreSQL

Ten business questions were answered using structured SQL queries:

| # | Question | Key Result |
|---|---|---|
| 1 | Revenue by gender | Male: $157,890 vs Female: $75,191 |
| 2 | High-spending discount users | 839 customers spent above average while using a discount |
| 3 | Top 5 products by rating | Gloves (3.86), Sandals (3.84), Boots (3.82) |
| 4 | Shipping type comparison | Express avg: $60.48 vs Standard avg: $58.46 |
| 5 | Subscribers vs non-subscribers | Avg spend nearly equal ($59.49 vs $59.87) |
| 6 | Discount-dependent products | Hat (50%), Sneakers (49.7%), Coat (49.1%) |
| 7 | Customer segmentation | Loyal: 3,116 / Returning: 701 / New: 83 |
| 8 | Top 3 products per category | Jewelry, Blouse, Sandals, Jacket lead their categories |
| 9 | Repeat buyers and subscriptions | 2,518 repeat buyers are NOT subscribed |
| 10 | Revenue by age group | Young Adults lead at $62,143 |

---

## Power BI Dashboard

An interactive dashboard was built to present the findings visually. Filters include Subscription Status, Gender, Product Category, and Shipping Type.

**Dashboard KPIs:**
- Total customers: 3.9K
- Average purchase amount: $59.76
- Average review rating: 3.75

**Visuals included:**
- Subscription status donut chart (Yes 27% / No 73%)
- Revenue and sales by product category (bar charts)
- Revenue and sales by age group (bar charts)

---

## Key Findings

- **Male customers drive 2x more revenue** than female customers despite similar average order values, reflecting a larger purchase volume.
- **80% of customers are Loyal** (5+ purchases). The business has a strong retention base.
- **2,518 repeat buyers are not subscribed**, representing the single biggest conversion opportunity.
- **Young Adults are the top-spending age group** at $62,143 in total revenue.
- **Hat, Sneakers, and Coat** have the highest discount dependency (48-50%), suggesting customers in these categories are trained to wait for promotions.
- **Express shipping users spend slightly more** per order ($60.48 vs $58.46), suggesting a higher-intent buyer segment.

---

## Business Recommendations

1. **Convert repeat non-subscribers** — Run a targeted campaign for the 2,518 loyal non-subscribers. Even a 10% conversion would meaningfully grow recurring revenue.
2. **Launch a loyalty reward program** — With 80% of customers already classified as Loyal, a tiered rewards system would increase retention and average order value.
3. **Review the discount strategy** — Products like Hat, Sneakers, and Coat have near 50% discount rates. Consider time-limited promotions instead of persistent discounts to protect margins.
4. **Target Young Adults and Male customers** — These groups deliver the highest revenue. Prioritize them in new product launches and premium campaigns.
5. **Feature top-rated products prominently** — Gloves, Sandals, and Boots have the highest customer satisfaction scores and should be highlighted in email campaigns and on the homepage.

---

## How to Run

**Prerequisites:**
- Python 3.8+
- PostgreSQL (running locally or via Docker)
- Power BI Desktop (for the dashboard file)

**Steps:**

```bash
# 1. Clone the repository
git clone https://github.com/your-username/customer-trends-data-analysis-SQL-Python-PowerBI.git
cd customer-trends-data-analysis-SQL-Python-PowerBI

# 2. Install Python dependencies
pip install pandas psycopg2-binary sqlalchemy jupyter

# 3. Set up your PostgreSQL connection
# Update the connection string in the notebook or script:
# postgresql://username:password@localhost:5432/your_database

# 4. Run the notebook
jupyter notebook analysis.ipynb

# 5. Open the Power BI dashboard
# Open dashboard.pbix in Power BI Desktop
```

---

## Project Structure

```
customer-trends-data-analysis-SQL-Python-PowerBI/
│
├── data/
│   └── shopping_trends.csv          # Raw dataset
│
├── notebooks/
│   └── analysis.ipynb               # Python cleaning and EDA
│
├── sql/
│   ├── 01_revenue_by_gender.sql
│   ├── 02_high_spending_discount_users.sql
│   ├── 03_top_products_by_rating.sql
│   ├── 04_shipping_type_comparison.sql
│   ├── 05_subscribers_vs_non_subscribers.sql
│   ├── 06_discount_dependent_products.sql
│   ├── 07_customer_segmentation.sql
│   ├── 08_top_products_per_category.sql
│   ├── 09_repeat_buyers_subscriptions.sql
│   └── 10_revenue_by_age_group.sql
│
├── dashboard/
│   └── dashboard.pbix               # Power BI dashboard file
│
└── README.md
```

---

## Author

Built as a portfolio project to demonstrate a full retail analytics workflow from raw data to business insights.

Feel free to fork, use, or reach out with questions.
