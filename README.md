# customer_behavior_analysis
End-to-end customer behavior analytics using Python, PostgreSQL, and Power BI — from data pipeline to interactive dashboard.
# 🛍️ Customer Shopping Behavior Analysis

A complete end-to-end data analytics project analyzing customer shopping patterns, purchasing habits, and revenue trends — from raw data to an interactive Power BI dashboard.

---

## 📌 Overview

This project explores a retail customer dataset to uncover actionable business insights around customer segmentation, product performance, discount effectiveness, and revenue contribution. The workflow covers every stage of a real-world analytics pipeline: data loading, exploratory analysis, cleaning, SQL-based querying, and visual reporting.

**Key business questions answered:**
- Do subscribed customers spend more than non-subscribers?
- Which products and categories drive the most revenue?
- How do discount strategies affect purchasing behavior?
- What customer segments (New, Returning, Loyal) exist in the data?
- Which age groups contribute the most revenue?

---

## 📂 Dataset

| Property | Details |
|---|---|
| **File** | `customer_shopping_behavior.csv` |
| **Records** | 3,900 customers |
| **Features** | 18 columns (demographics, purchase history, product info, shipping, subscription) |

**Key columns include:** `customer_id`, `age`, `gender`, `category`, `item_purchased`, `purchase_amount`, `review_rating`, `subscription_status`, `discount_applied`, `frequency_of_purchases`, `previous_purchases`, `shipping_type`

---

## 🛠️ Tools & Technologies

| Layer | Tool |
|---|---|
| **Language** | Python 3 |
| **Data Analysis** | Pandas |
| **Database** | PostgreSQL |
| **ORM / Connector** | SQLAlchemy, psycopg2 |
| **Visualization** | Power BI |
| **Notebook** | Jupyter Notebook |
| **Version Control** | Git & GitHub |

---

## 🔄 Project Steps

### 1. 📥 Data Loading
- Loaded the CSV dataset into a Pandas DataFrame
- Performed an initial inspection using `.head()`, `.info()`, and `.describe()`

### 2. 🔍 Exploratory Data Analysis (EDA)
- Checked data types, column distributions, and summary statistics
- Identified missing values across all columns
- Verified data consistency (e.g., confirmed `discount_applied` and `promo_code_used` were always identical)

### 3. 🧹 Data Cleaning
- **Handled nulls:** Imputed missing `review_rating` values using category-level median — a context-aware strategy that avoids skewing ratings
- **Standardized columns:** Lowercased all column names and replaced spaces with underscores for SQL compatibility
- **Renamed columns:** `purchase_amount_(usd)` → `purchase_amount` for cleaner querying
- **Feature engineering:**
  - Created `age_group` using quartile-based binning (`Young Adult`, `Adult`, `Middle-aged`, `Senior`)
  - Created `purchase_frequency_days` by mapping text frequency labels (e.g., `Weekly` → `7`, `Monthly` → `30`) to numeric values
- **Dropped redundant column:** Removed `promo_code_used` as it was a duplicate of `discount_applied`

### 4. 🗄️ Database Integration
- Connected to a local PostgreSQL database using SQLAlchemy
- Loaded the cleaned DataFrame into a `customer` table using `.to_sql()`
- All subsequent analysis was performed via SQL queries

### 5. 🧮 SQL Analysis
Queries were written to answer targeted business questions:

| Query | Purpose |
|---|---|
| Revenue by gender | Compare male vs female spending |
| High-value discount users | Find customers using discounts but spending above average |
| Top-rated products | Identify the 5 highest-rated items |
| Shipping type vs spend | Compare average spend across Standard and Express shipping |
| Subscriber vs non-subscriber | Revenue and avg spend comparison |
| Discount rate by product | Which products are most frequently discounted? |
| Customer segmentation | Classify customers as New / Returning / Loyal |
| Top 3 products per category | Window function with `ROW_NUMBER()` and `PARTITION BY` |
| Repeat buyers & subscription | Are repeat buyers more likely to subscribe? |
| Revenue by age group | Which age segment drives the most revenue? |

### 6. 📊 Power BI Dashboard
- Connected Power BI to the PostgreSQL database
- Built an interactive dashboard with Card, Custome column chart,Donut chart and Button Slicer
- Visualized key metrics including revenue by segment, product performance, and subscription impact
  
 ### 7. 📝 Report
- Compiled findings into a structured report summarizing insights, business recommendations, and limitations

---
## 📊 Dashboard Preview

> *Power BI dashboard screenshot —  <img width="1438" height="831" alt="Screenshot 2026-05-04 at 8 09 23 PM" src="https://github.com/user-attachments/assets/741d4e0a-5c93-4fae-aeac-f5dede00221c" />
*

**Dashboard highlights:**
- 💰 Total revenue breakdown by gender, age group, and subscription status
- 🏆 Top 5 products by revenue and review rating
- 🔖 Discount usage rates by product and category
- 👥 Customer segment distribution (New / Returning / Loyal)
- 📦 Shipping preference vs average spend

---

## 📈 Key Results

| Insight | Finding |
|---|---|
| **Subscription impact** | Subscribed customers generate higher total revenue and a higher average spend per transaction |
| **Top customer segment** | Loyal customers (10+ purchases) represent the largest revenue-generating group |
| **Discount effectiveness** | Discounted purchases do not significantly reduce average spend — high-value customers still spend above average with discounts |
| **Best-rated products** | The top 5 products by review rating span multiple categories, suggesting broad customer satisfaction |
| **Age group revenue** | Middle-aged customers (based on quartile binning) contribute the highest share of total revenue |
| **Shipping vs spend** | No significant average spend difference between Standard and Express shipping customers |

---

## ▶️ How to Run

### Prerequisites
Make sure you have the following installed:
- Python 3.8+
- PostgreSQL (running locally or via a cloud instance)
- Power BI Desktop (Windows)
- Jupyter Notebook or JupyterLab

### Step 1 — Clone the Repository
```bash
git clone https://github.com/your-username/customer-shopping-behavior-analysis.git
cd customer-shopping-behavior-analysis
```

### Step 2 — Install Python Dependencies
```bash
pip install pandas sqlalchemy psycopg2-binary jupyter
```

### Step 3 — Set Up PostgreSQL
1. Create a database named `customer_behavior` in PostgreSQL
2. Update the connection details in the notebook:
```python
username = "your_username"
password = "your_password"
host     = "localhost"
port     = "5432"
database = "customer_behavior"
```

### Step 4 — Run the Notebook
```bash
jupyter notebook Customer_Shopping_Behavior_Analysis.ipynb
```
Run all cells from top to bottom. The cleaned data will be automatically loaded into your PostgreSQL database.

### Step 5 — Run the SQL Queries
Open `customer_behavior.sql` in your preferred SQL client (pgAdmin, DBeaver, etc.) and run the queries against the `customer_behavior` database.

### Step 6 — Open the Power BI Dashboard
1. Open the `.pbix` file in Power BI Desktop
2. Update the data source to point to your PostgreSQL instance
3. Refresh the data

---

## 📁 Project Structure

```
customer-shopping-behavior-analysis/
│
├── Customer_Shopping_Behavior_Analysis.ipynb   # Python EDA & data cleaning
├── customer_behavior.sql                       # SQL queries for analysis
├── customer_shopping_behavior.csv              # Raw dataset
├── dashboard.pbix                              # Power BI dashboard file
├── report.pdf                                  # Final insights report
└── README.md                                   # Project documentation
```

---

## 👤 Author

**Ashwini Nerker**
📧 nerkerashwini.93@gmail.com
🔗 [LinkedIn]([(https://www.linkedin.com/in/ashwini-nerker-a29510159/))] | [GitHub]([https://github.com/Ashu-93])

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
