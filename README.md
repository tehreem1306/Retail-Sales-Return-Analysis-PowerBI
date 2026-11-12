# Retail Sales & Return Performance Analysis (Power BI)

## 📌 Project Overview
This end-to-end Business Intelligence project analyzes three years of retail sales and return performance (January 2022 – December 2024) for **Lotus Group**, a multi-store retail chain operating across 13 governorates in Egypt. 

Rather than working with pre-cleaned data, this project simulates a real-world ETL and BI workflow—transforming raw, messy CSV files into a validated **Star Schema** data model and building an interactive executive Power BI dashboard to uncover revenue trends and root causes of product returns.

---

## 🎯 Business Problem
High return volumes directly erode retail profit margins and operational efficiency. Leadership needs clear visibility into:
- How overall revenue and order volume perform across product categories (*Clothing* vs. *Electronics*).
- What percentage of revenue is lost to product returns, and what the primary drivers behind those returns are.
- How sales trends fluctuate over time across different years and months (2022–2024).

---

## 🗂 Dataset & Architecture
The analysis is built on the **Lotus Group Retail Dataset** (9 raw CSV files, 42,877 total rows, 12,000 orders, and 25,099 line-item transactions):

- **Fact Tables:** `fact_orders_2022_2023`, `fact_orders_2024` (appended into a unified orders table), `fact_order_details` (revenue source of truth), and `fact_returns`.
- **Dimension Tables:** `dim_products`, `dim_customers`, `dim_stores`, `dim_employees`, and `dim_date`.

---

## 🧹 Data Cleaning & ETL (Power Query)
Before modeling, extensive data profiling and transformation were performed in Power Query to resolve embedded data quality issues:
- **Appending & Merging:** Combined split yearly order tables (`2022_2023` + `2024`) using **Append Queries** and integrated return records via **Merge Queries**.
- **Deduplication & Null Handling:** Removed 50 exact duplicate customer rows in `dim_customers` and handled missing values (~12% in `email` and ~5% in `employee_id`).
- **Text & Delimiter Splitting:** Split combined fields (`full_name` in `dim_customers` and `product_name_raw` in `dim_products`) into clean, structured attributes.
- **Standardization & Formatting:** Trimmed leading/trailing whitespace (`phone`, `payment_method`), standardized inconsistent text casing (`gender`), converted text-stored dates (`birth_date`) to proper Date types, and stripped currency prefixes (`"EGP "`) from `unit_price_text` to convert into numeric currency values.

---

## 🔗 Data Modeling (Star Schema)
- Designed a **Star Schema** connecting dimension tables (`dim_products`, `dim_stores`, `dim_date`, `dim_customers`, `dim_employees`) to central fact tables (`fact_orders` and `fact_order_details`).
- Configured active relationships and optimized cross-filter directions (**Both**) between `dim_products`, `fact_order_details`, and `fact_orders` so category slicers dynamically filter both line-item revenue and order-level return KPIs.
- Configured visual-level **Edit Interactions** (Filter mode) to ensure seamless cross-filtering without visual distortion.

---

## 📊 Key Metrics & Business Insights
- **Overall Performance (2022–2024):** Generated **$45.35M** in Total Revenue across **12K** Total Orders, with **$4.01M** in Total Return Amount (**1,056** return orders — ~8.8% revenue return rate)[cite: 7].
- **Category Breakdown:**
  - **Clothing:** **$37.20M** revenue | **$3.28M** return amount | **998** return orders.
  - **Electronics:** **$36.31M** revenue | **$3.19M** return amount | **220** return orders[cite: 6].
- **Primary Return Drivers:** 
  - **Duplicate Order** is the leading cause of returns across the business (**21.37%** / **$857.43K**), followed by **Changed Mind** (**18.42%** / **$739.37K**) and **Quality Issue** (**16.27%** / **$652.84K**)[cite: 7].
  - *Actionable Recommendation:* Implementing duplicate-order warnings at checkout and improving pre-purchase product sizing/specification guides can recover a significant portion of the $4.01M return loss[cite: 7].

---

## 💡 Key Learnings & Takeaways
Through building this project, I gained hands-on experience in solving real-world data challenges:
- **End-to-End ETL Mastery:** Learned how to take raw, messy datasets containing missing values, duplicates, and unformatted strings and transform them into clean, analysis-ready tables using Power Query.
- **Relational Data Modeling:** Gained a deep understanding of Star Schema design, managing cardinalities (*:1), and handling bi-directional cross-filtering to ensure accurate propagation of slicer filters across complex fact-dimension relationships.
- **Translating Data to Business Value:** Realized that data analytics is not just about building dashboards, but about uncovering root causes (such as tracking product return drivers) to provide actionable business recommendations.

---

## 🛠 Tools & Technologies
- **Power BI Desktop** (Dashboard Design, Custom UI/UX, Edit Interactions)
- **Power Query (M)** (ETL, Data Cleaning, Append/Merge Transformations)
- **Data Modeling** (Star Schema, Cardinality & Cross-Filter Management)
- **DAX** (KPI Measures & Aggregations)
- **Git & GitHub** (Version Control & Project Documentation)

---

## 📁 Project Structure
```text
retail-sales-return-dashboard/
│
├── Retail_Sales_Return_Dashboard.pbix    # Interactive Power BI Report
├── Dashboard_Demo.mp4                    # Screen recording of interactive slicers & KPIs
├── README.md                             # Project documentation & business insights
└── screenshots/                          # High-resolution dashboard views
