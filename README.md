# 🛍️ Customer Shopping Behaviour Analysis

### An End-to-End Data Analytics Project — Python · PostgreSQL · Power BI

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](#license)

> A complete data analytics pipeline that transforms 3,900 raw retail transaction records into decision-ready business insight — from data cleaning in **Python**, to structured business-question analysis in **SQL**, to an interactive, self-service **Power BI dashboard**.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Findings at a Glance](#-key-findings-at-a-glance)
- [Project Architecture](#-project-architecture)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Methodology](#-methodology)
- [Business Questions Answered](#-business-questions-answered)
- [Power BI Dashboard](#-power-bi-dashboard)
- [How to Reproduce](#-how-to-reproduce)
- [Recommendations](#-recommendations)
- [Future Work](#-future-work)
- [Author](#-author)

---

## 📖 Overview

Understanding **what customers buy, how much they spend, and what drives loyalty** is central to any effective retail strategy. This project analyzes a real-world-style customer shopping behaviour dataset to answer **10 targeted business questions** spanning revenue drivers, product performance, discounting behaviour, and customer segmentation.

The project mirrors a standard **industry end-to-end analytics workflow**:

1. **Clean & engineer** raw transactional data using Python (`pandas`) in Jupyter.
2. **Query & analyze** the cleaned data in a **PostgreSQL** relational database using SQL.
3. **Visualize** the results in an interactive **Power BI** dashboard for ongoing, self-service monitoring.
4. **Synthesize** everything into a formal business report with actionable recommendations.

---

## 🔑 Key Findings at a Glance

| Insight | Detail |
|---|---|
| 👨‍👩‍👧 **Gender revenue gap** | Male customers drive **68% of transactions** and **$157,890 (67.7%)** of revenue — more than double female customers ($75,191). |
| 👗 **Category leader** | **Clothing** leads with **$104,264** in revenue (44.7% of total), followed by Accessories ($74,200). |
| 🚚 **Shipping** | Express shipping customers spend marginally more on average (**$60.48**) than Standard (**$58.46**). |
| 🏷️ **Discounting** | **839 customers** used a discount and *still* spent at/above the $59.76 average — discounts don't universally suppress order value. |
| 🔁 **Loyalty-driven base** | **79.9%** of customers fall into the "Loyal" segment (10+ previous purchases) — a highly repeat-driven customer base. |
| 📬 **Subscriptions** | Subscribers ($59.49 avg) don't meaningfully out-spend non-subscribers ($59.87 avg) per order — subscription isn't a strong revenue differentiator on its own. |
| 🎂 **Age groups** | **Young Adults** are the top revenue-contributing age group at **$62,143**, narrowly ahead of Middle-Aged customers. |
| 📅 **Seasonality** | Revenue is well-balanced across seasons ($55.8K–$60.0K, a spread of just 7.6%) — demand is non-seasonal and stable. |
| 💳 **Payment methods** | Highly balanced usage (Credit Card & PayPal marginally lead) — no channel should be deprioritized. |

> 📄 Full methodology, SQL queries, and supporting visuals for each finding are documented in [`Customer_Behaviour_Analysis_Report.docx`](./Customer_Behaviour_Analysis_Report.docx).

---

## 🏗️ Project Architecture

```
┌─────────────────────┐      ┌──────────────────────┐      ┌────────────────────────┐
│   Raw CSV Dataset    │ ───▶ │  Python / pandas      │ ───▶ │  PostgreSQL Database    │
│  3,900 transactions  │      │  Cleaning + Feature   │      │  Loaded via SQLAlchemy  │
│  18 attributes       │      │  Engineering          │      │                         │
└─────────────────────┘      └──────────────────────┘      └────────────┬────────────┘
                                                                          │
                                                                          ▼
                              ┌──────────────────────┐      ┌────────────────────────┐
                              │   Power BI Dashboard  │ ◀─── │  SQL Business Analysis  │
                              │  Interactive, self-   │      │  10 targeted queries    │
                              │  service exploration  │      │                         │
                              └──────────────────────┘      └─────────────────────────┘
```

---

## 🗂️ Dataset

| Attribute | Detail |
|---|---|
| **Records** | 3,900 unique customer transactions |
| **Columns** | 18 attributes |
| **Coverage** | 50 U.S. locations, ages 18–70 |
| **Categories** | Demographics, product details, transaction data, behavioural indicators |
| **Data quality** | Zero duplicate customer IDs; zero missing values after cleaning |

**Key fields:** `age`, `gender`, `item_purchased`, `category`, `purchase_amount`, `location`, `review_rating`, `subscription_status`, `shipping_type`, `discount_applied`, `previous_purchases`, `payment_method`, `frequency_of_purchases`.

---

## 🛠️ Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| **Data Wrangling** | Python (pandas, Jupyter) | Cleaning, feature engineering, null handling |
| **Database** | PostgreSQL + SQLAlchemy | Structured storage & querying |
| **Analysis** | SQL | 10 targeted business questions |
| **Visualization** | Microsoft Power BI | Interactive, filterable dashboard |
| **Reporting** | Microsoft Word | Consolidated business report |

---

## 📁 Repository Structure

```
├── customer_shopping_behavior.csv           # Raw source dataset (3,900 rows × 18 cols)
├── customer_behaviour_analysis.ipynb        # Python data cleaning & feature engineering
├── SQL_Analysis.sql                         # 10 business-question SQL queries (PostgreSQL)
├── Customer_Behaviour_Dashboard.pbix        # Interactive Power BI dashboard
├── Customer_Behaviour_Analysis_Report.docx  # Full consolidated business report
├── Code_to_Connect_Jupyter_To_PostgreS.txt  # SQLAlchemy connection snippet
└── README.md                                # You are here
```

---

## 🔬 Methodology

### 1. Data Preparation — Python (`pandas`)
- Profiled the raw dataset using `.info()`, `.describe()`, and `.isnull().sum()` to identify structural issues.
- Imputed missing `review_rating` values using the **median rating within each product category**, preserving category-level tendencies rather than a single global median.
- Standardized all column headers to lowercase `snake_case` for consistency and SQL compatibility.
- Renamed the ambiguous `purchase_amount_(usd)` column to `purchase_amount`.
- Engineered an **`age_group`** feature — quartile-based bins: *Young Adult, Adult, Middle-Aged, Senior*.
- Engineered a **`purchase_frequency_days`** feature, converting categorical frequency labels (e.g. "Weekly", "Fortnightly") into a numeric day-count.
- Identified that `promo_code_used` and `discount_applied` were fully duplicative columns and dropped the redundant one.
- Loaded the cleaned dataset into **PostgreSQL** via SQLAlchemy for structured querying.

### 2. Business Analysis — SQL (PostgreSQL)
Ten targeted business questions were answered directly against the cleaned `customer` table — see [Business Questions Answered](#-business-questions-answered) below.

### 3. Visualization — Power BI
An interactive dashboard was built on the cleaned dataset with dynamic slicers, cross-filtering visuals, and real-time KPI cards — enabling non-technical stakeholders to explore the same insights without writing SQL.

---

## ❓ Business Questions Answered

| # | Question |
|---|---|
| 1 | What is the total revenue generated by male vs. female customers? |
| 2 | Which customers used a discount but still spent more than the average purchase amount? |
| 3 | What are the top 5 products with the highest average review rating? |
| 4 | How does average spend compare between Standard and Express shipping? |
| 5 | Do subscribed customers spend more than non-subscribers? |
| 6 | Which 5 products have the highest percentage of discounted purchases? |
| 7 | How do customers segment into New, Returning, and Loyal buyers? |
| 8 | What are the top 3 best-selling products within each category? |
| 9 | Are repeat buyers (5+ previous purchases) more likely to subscribe? |
| 10 | What is the revenue contribution of each age group? |

All queries are available in [`SQL_Analysis.sql`](./SQL_Analysis.sql), with results and visual interpretation documented in the full report.

<details>
<summary><strong>📋 Example query — Revenue by Gender</strong></summary>

```sql
SELECT gender, SUM(purchase_amount) AS revenue
FROM customer
GROUP BY gender;
```
</details>

---

## 📊 Power BI Dashboard

The dashboard (`Customer_Behaviour_Dashboard.pbix`) mirrors the core SQL analysis in a fully interactive, self-service format:

- 🎛️ **Dynamic slicers** for gender, category, season, location, and payment method
- 🔗 **Cross-filtering visuals** — selecting one element instantly updates all other visuals
- 📈 **Real-time KPI cards** for total revenue, average order value, transaction count, and average review rating
- 🔄 **Refreshable data model** — designed to reflect new transactions without rebuilding visuals

> Open the `.pbix` file in Power BI Desktop to explore the dashboard interactively.

---

## ▶️ How to Reproduce

### Prerequisites
- Python 3.x, Jupyter Notebook
- PostgreSQL (local or hosted) + `pgAdmin` (optional)
- Power BI Desktop (Windows)

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/customer-shopping-behaviour-analysis.git
cd customer-shopping-behaviour-analysis

# 2. Install Python dependencies
pip install pandas sqlalchemy psycopg2-binary jupyter

# 3. Launch the notebook
jupyter notebook customer_behaviour_analysis.ipynb
```

Update the PostgreSQL connection details in the notebook / `Code_to_Connect_Jupyter_To_PostgreS.txt` with your own credentials, then run the notebook end-to-end to load the cleaned data into your database. Once loaded, execute the queries in `SQL_Analysis.sql`, or open `Customer_Behaviour_Dashboard.pbix` in Power BI Desktop to explore the pre-built dashboard.

> ⚠️ **Note:** Database credentials in the included connection script are placeholders and should be replaced with your own local values — never commit real credentials to source control.

---

## 💡 Recommendations

1. **Investigate the gender revenue gap** — pilot targeted campaigns to grow female customer acquisition and basket size, given the current 68/32 transaction split.
2. **Convert high-frequency non-subscribers** — repeat buyers (5+ purchases) subscribe at the same ~27% rate as the general population; target this proven-loyal group with subscription incentives.
3. **Audit discount strategy** on high-discount-rate items (Hat, Sneakers, Coat, Sweater, Pants) to confirm promotions drive incremental volume rather than eroding margin unnecessarily.
4. **Prioritize new-customer acquisition** — at only ~2.1% of the base, new-customer growth is under-indexed relative to retention efforts.
5. **Leverage top-rated products** (Gloves, Sandals, Boots, Hat, Skirt) in featured placements and marketing creative.
6. **Adopt the Power BI dashboard** for ongoing, self-service monitoring between formal reporting cycles.

---

## 🔮 Future Work

- Extend the dataset to **multiple transactions per customer** to properly measure lifetime value and repeat-purchase frequency.
- Layer in **cohort analysis** to track how the New → Returning → Loyal pipeline evolves over time.
- Add **profitability (cost/margin) data** to complement the revenue-only view, enabling true ROI assessment of discount and shipping strategies.

---

## 👤 Author

**Vikram Kumar**
📧 connectwithvikramkumar@gmail.com · 🔗 [LinkedIn](#) · 💻 [Portfolio](#)

If you found this project useful, consider giving it a ⭐ on GitHub!

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
