# 🧠 E-Commerce Customer Behaviour Analysis

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0%2B-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)

An end-to-end data analytics and SQL engineering project investigating customer purchasing patterns, category revenue concentration, payment behavior, regional distribution, and repeat buyer trends using **Python**, **MySQL 8**, **Pandas**, **Matplotlib**, and **Seaborn**.

Designed for a **Data Analyst & Analytics Engineer Portfolio**, this project demonstrates rigorous SQL data modeling, fan-out error prevention, automated data quality reconciliation, and data-driven business storytelling.

---

## 📌 Business Questions Addressed

1. **Order Volume & Fulfillment Trends:** How do overall monthly order volumes and delivered fulfillment rates evolve over time?
2. **Product Category & Seller Rankings:** Which product categories and top merchants drive the highest delivered item sales?
3. **Credit Financing & Payment Behaviour:** What proportion of customers utilize multiple installments for credit financing?
4. **Geographic Distribution & Basket Size:** Where are customers concentrated, and how does average basket size vary across cities and states?
5. **Repeat Buyer Behaviour:** How do repeat buyers compare with one-time customers in order frequency and average spend?

---

## 🗂️ Dataset & Relational Architecture

The analysis is based on the [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), comprising seven relational tables:

| Table | File Name | Primary Key | Foreign Keys | Description |
| :--- | :--- | :--- | :--- | :--- |
| **`customers`** | `customers.csv` | `customer_id` | N/A | Maps order-level `customer_id` to persistent `customer_unique_id`. |
| **`orders`** | `orders.csv` | `order_id` | `customer_id` | Order lifecycle records, status, and purchase timestamps. |
| **`order_items`** | `order_items.csv` | `(order_id, order_item_id)` | `order_id`, `product_id`, `seller_id` | Line-item product prices and freight charges. |
| **`payments`** | `payments.csv` | `(order_id, payment_sequential)` | `order_id` | Payment methods, installment counts, and transaction values. |
| **`products`** | `products.csv` | `product_id` | N/A | Catalog metadata and product categories (`product_category`). |
| **`sellers`** | `sellers.csv` | `seller_id` | N/A | Merchant directory and location (`seller_city`, `seller_state`). |
| **`geolocation`** | `geolocation.csv` | N/A | N/A | Geolocation ZIP code prefix coordinates. |

---

## 🛠️ Data Engineering & Analytical Rigor

* **Fan-Out Error Prevention:** Joining 1-to-many `order_items` and `payments` directly duplicates payment totals. Queries aggregate split payments at the `order_id` level first before joining to orders.
* **Customer Identity Granularity:** Distinguishes session-level `customer_id` from stable individual identity `customer_unique_id` for accurate repeat customer tracking.
* **Automated Financial Reconciliation:** Verifies that category sales, seller rankings, and monthly payment sums match independent database baselines down to `R$ 0.00` discrepancy.
* **SQL Window Functions:** Utilizes advanced window functions (`SUM() OVER (PARTITION BY year ORDER BY month)` and `AVG() OVER (ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)`) for cumulative YTD tracking and trailing averages.

---

## 📈 Key Verified Portfolio Findings

All metrics were computed directly from the dataset and verified against database baselines:

* 🛍️ **Category Concentration:** Total delivered item sales reached **R$ 13,221,498.11**. `HEALTH BEAUTY` was the top category (**R$ 1,233,131.72**, 9.33% share), followed by `Watches present` (**R$ 1,166,176.98**, 8.82% share), `bed table bath` (**R$ 1,023,434.76**, 7.74% share), and `sport leisure` (**R$ 954,852.55**, 7.22% share).
* 💳 **High Credit Financing:** Out of **96,477** delivered orders with payments, **49,661 orders (51.47%)** were paid using multiple installments (`payment_installments > 1`), highlighting credit financing as a primary purchasing mechanism.
* 📍 **Geographic Concentration:** São Paulo (`SP`) leads customer concentration with **40,302 unique customers** (40.5% of overall base) and **41,746 orders**, followed by Rio de Janeiro (`RJ`, 12,384 customers) and Minas Gerais (`MG`, 11,259 customers).
* 🔄 **Repeat Buyer Dynamics:** Out of 93,357 delivered customer identities, **2,801 (3.00%)** were repeat buyers in the observed window, averaging **R$ 145.98** per order compared to **R$ 160.76** for one-time buyers.

---

## 💻 Tech Stack & Requirements

- **Language:** Python 3.10+
- **Database:** MySQL 8.0+ (with automatic SQLite fallback)
- **Libraries:** Pandas, Matplotlib, Seaborn, MySQL Connector Python, Python-Dotenv, JupyterLab

```text
Customer-Behaviour-Analysis/
│
├── customers.ipynb       # Main executable Jupyter Notebook (Analysis, SQL & Charts)
├── README.md             # Project documentation & business overview
├── requirements.txt      # Python dependencies
├── .env.example          # Database configuration template
└── .gitignore            # Git ignore rules for credentials, data, and cache
```

---

## 🚀 Quickstart Guide

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/omrohitchannoji/Customer-Behaviour-Analysis.git
cd Customer-Behaviour-Analysis
```

### 2️⃣ Environment Setup
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
```

### 3️⃣ Configure Database Credentials
Edit `.env` to match your local MySQL settings:
```ini
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=your_password
MYSQL_DATABASE=ecommerce
```

### 4️⃣ Run the Notebook
Launch Jupyter Notebook and run all cells:
```bash
jupyter lab customers.ipynb
```

---

## 👨‍💻 Author

**Omrohit Channoji**  
*Data Analyst & Analytics Engineer*  
📧 Email: omrohitchannoji7@gmail.com  
🌐 GitHub: [github.com/omrohitchannoji](https://github.com/omrohitchannoji)
