# Customer Shopping Behavior Analysis

An end-to-end data analytics project analyzing customer purchasing patterns across **3,900 transactions**. This project demonstrates an end-to-end analytics workflow: data cleaning and EDA in Python, automated database ingestion into PostgreSQL, structured business analysis via SQL, interactive visualization in Power BI, and executive presentation delivery via PDF and PowerPoint.

---

## 📌 Project Overview
The objective of this project is to analyze consumer behavior to uncover key drivers behind revenue, customer retention, subscription adoption, and promotional effectiveness. 

**Key Insights Uncovered:**
* **Revenue Drivers:** Male customers generated **$157,890** in total revenue compared to **$75,191** from female customers, with **Young Adults** contributing the highest share ($62,143).
* **Subscription Gap:** Subscription adoption sits at **27%** (1,053 subscribers vs. 2,847 non-subscribers). However, average spend remains nearly identical ($59.49 vs. $59.87), highlighting a penetration opportunity rather than an order-value gap.
* **Discount Dependence:** Products like **Hats (50.0%)** and **Sneakers (49.7%)** exhibit high discount sensitivity, requiring improved margin discipline.

---

## 📊 Dataset Summary
* **Records:** 3,900 customer transactions
* **Attributes:** 18 features (Demographics, Transaction Details, Product Categories, Behavioral Metrics)
* **Key Features:** `age`, `gender`, `category`, `item_purchased`, `purchase_amount`, `review_rating`, `subscription_status`, `shipping_type`, `discount_applied`, `previous_purchases`

---

## 🛠️ Tools & Technologies Used
* **Python (Jupyter Notebook):** Pandas, NumPy, SQLAlchemy, Psycopg2 (Data Cleaning, Feature Engineering, Imputation)
* **PostgreSQL & pgAdmin:** Relational database storage, Window functions, CTEs, Aggregations, Business logic validation
* **Power BI:** Interactive Dashboard creation, DAX measures, Data modeling, Dynamic Slicers
* **PowerPoint / PDF:** Executive summary slide deck for stakeholder readouts

---

## 🚀 Execution Steps

### 1. Data Cleaning & EDA (Python)
* **Missing Value Imputation:** Handled 37 missing `review_rating` values by imputing category-level median ratings.
* **Standardization:** Converted column names to `snake_case` and renamed `purchase_amount_(usd)` to `purchase_amount`.
* **Feature Engineering:**
  * Created `age_group` bins (*Young Adult, Adult, Middle-aged, Senior*).
  * Mapped purchase frequencies to numeric intervals (`purchase_frequency_days`).
* **Redundancy Removal:** Dropped `promo_code_used` after verifying 100% correlation with `discount_applied`.

### 2. Database Integration & Ingestion
* Established a database connection from Jupyter Notebook to **PostgreSQL** using `sqlalchemy` and `psycopg2`.
* Automatically exported the cleaned Pandas DataFrame into the PostgreSQL `customer` table.

```python
from sqlalchemy import create_engine

engine = create_engine('postgresql+psycopg2://username:password@localhost:5432/customer_behavior')
df.to_sql('customer', engine, if_exists='replace', index=False)
```

### 3. Business Analysis (SQL Queries)
Executed SQL queries in PostgreSQL to solve core business problems:
* **Customer Segmentation:** Categorized buyers into *New (1 purchase)*, *Returning (2-10 purchases)*, and *Loyal (>10 purchases)* segments (**3,116 Loyal customers** identified).
* **Discount-Heavy Buyers:** Identified **839 high-spending customers** who purchased using discounts but still spent above the global average purchase amount ($59.76).
* **Category Rankings:** Utilized `ROW_NUMBER() OVER(PARTITION BY category ...)` to rank the top 3 selling items per category (e.g., Jewelry, Sunglasses, and Belts leading Accessories).

### 4. Interactive Dashboarding (Power BI)
* Connected Power BI to PostgreSQL directly.
* Designed an interactive layout featuring KPI cards, sales by category, revenue by age groups, subscription breakdowns, and multi-field slicers (*Gender, Category, Shipping Type*).

---

## 📈 Key Results & Recommendations

1. **Promote Subscription Value:** 2,518 repeat buyers (>5 purchases) are currently non-subscribers. Offer exclusive loyalty perks to convert repeat buyers into subscribers.
2. **Optimize Promotional Strategy:** High discount rates on items like Hats and Sneakers indicate a risk of margin erosion. Replace blanket promotions with targeted upsell offers.
3. **Target High-Value Demographics:** Focus acquisition marketing on **Young Adults** and **Middle-aged** segments, while highlighting top-rated products (*Gloves, Sandals, Boots*) in ad campaigns.

---

## 🖥️ Dashboard Preview
The Power BI dashboard provides dynamic visual insights into overall revenue performance, customer segmentation, category performance, and subscription adoption.

![image alt](https://github.com/MayankSingh2000/-customer-behavior-analysis/blob/main/customer_behavior_analysis_dashboard.png?raw=true)
---

## 💻 How to Run This Project

### Prerequisites
* Python 3.x with Jupyter Notebook
* PostgreSQL & pgAdmin
* Power BI Desktop

### Setup Instructions
1. **Clone the Repository:**
   ```bash
  https://github.com/MayankSingh2000/-customer-behavior-analysis
   ```bash

2. **Run Data Preparation (Python):**
   * Open `notebooks/Customer_Behavior_Analysis.ipynb`.
   * Ensure `psycopg2-binary` and `sqlalchemy` are installed:
     ```bash
     pip install pandas psycopg2-binary sqlalchemy
     ```
   * Update PostgreSQL credentials in the notebook and execute all cells to clean data and create the SQL table.

3. **Execute SQL Analysis:**
   * Import `sql/analysis_queries.sql` into pgAdmin / PostgreSQL and execute to run business queries.

4. **View Power BI Dashboard & Presentation:**
   * Open `reports/Customer_Behavior_Dashboard.pbix` in Power BI.
   * Review `reports/Customer_Shopping_Behavior_Analysis.pptx` for executive readout slides.

---

## 📁 Repository Structure
```text
├── data/
│   └── customer_shopping_behavior.csv    # Raw dataset
├── notebooks/
│   └── Customer_Behavior_Analysis.ipynb  # Data cleaning, EDA & DB push
├── sql/
│   └── analysis_queries.sql              # PostgreSQL business analysis queries
├── reports/
│   ├── Customer_Behavior_Dashboard.pbix  # Interactive Power BI file
│   ├── Customer_Behavior_Analysis.pdf    # Full project documentation report
│   └── Customer_Shopping_Behavior_Analysis.pptx # Executive PPT presentation
└── README.md                             # Project documentation
```
