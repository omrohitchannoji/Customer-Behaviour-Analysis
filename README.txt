# 🧠 Customer Behaviour Analysis

This project automates the process of converting multiple **raw CSV files** into a structured **MySQL database** using **Python and Pandas**, enabling seamless customer-behavior analysis.  
It acts as a complete **ETL (Extract, Transform, Load)** workflow — from CSV import → SQL table creation → data insertion → ready-to-query database for insights.

---

## 🚀 Project Overview

Businesses often store large customer and order data in separate CSV files (customers, orders, payments, products, etc.).  
This project:

- Loads and cleans all CSV datasets automatically  
- Creates corresponding SQL tables inside a MySQL database  
- Infers SQL data types dynamically  
- Inserts data efficiently for analysis  
- Enables customer-behavior insights using Python + SQL integration  

---

## 🧩 Key Features
✅ Batch import of multiple CSV files  
✅ Automatic SQL table creation with inferred column data types  
✅ Conversion of NaN values → NULL for SQL compatibility  
✅ Runs entirely in Python (no manual SQL needed)  
✅ Prepares a clean relational database for analytics and visualization  

---

## 🗂️ Project Structure
customer_behaviour_analysis/
│
├── customers.py # Main Python script
├── data/
│ ├── customers.csv
│ ├── orders.csv
│ ├── sellers.csv
│ ├── products.csv
│ ├── geolocation.csv
│ ├── payments.csv
│ └── order_items.csv
├── requirements.txt
└── README.md

---

## ⚙️ How It Works
1. The script loops through all CSV files listed in the configuration.  
2. Each file is read into a Pandas DataFrame.  
3. Column data types are automatically mapped to SQL equivalents (`INT`, `FLOAT`, `TEXT`, etc.).  
4. Tables are created in MySQL dynamically if they don’t already exist.  
5. Data is inserted into tables row-by-row, replacing missing values with SQL `NULL`.  
6. Once complete, the MySQL database (`ecommerce`) is ready for analytical queries.  

---

## 🧠 Tables Created
- `customers`  
- `orders`  
- `sellers`  
- `products`  
- `geolocation`  
- `payments`  
- `order_items`  

---

## 🔧 Setup Instructions

### 1️⃣ Clone the Repository

git clone https://github.com/omrohitchannoji/customer-behaviour-analysis.git
cd customer-behaviour-analysis

### 2️⃣ Install Dependencies
pip install -r requirements.txt

### 3️⃣ Update Database Configuration
conn = mysql.connector.connect(
    host='localhost',
    user='root',
    password='your_password',
    database='ecommerce'
)

### 4️⃣ Run the Script
python customers.py


🧾 requirements.txt
pandas
mysql-connector-python

📈 Example Analysis Ideas

Once the data is stored in SQL, you can run analytical queries in Python such as:

# Example 1: Top 10 customers by spending
query = """
SELECT customer_id, SUM(payment_value) AS total_spent
FROM payments
JOIN orders USING(order_id)
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 10;
"""

# Example 2: Average order value by state
query = """
SELECT g.geolocation_state, AVG(p.payment_value) AS avg_order_value
FROM payments p
JOIN orders o USING(order_id)
JOIN geolocation g ON o.customer_id = g.geolocation_zip_code_prefix
GROUP BY g.geolocation_state;
"""


These queries can be executed directly in Python using mysql.connector and visualized with Pandas or Matplotlib.

💡 Future Enhancements

Automate CSV discovery (read all .csv files in a folder automatically)

Add logging and error handling

Integrate Streamlit dashboard for visual insights

Store database credentials in environment variables for security

👨‍💻 Author

Omrohit Channoji
📧 omrohitchannoji7@gmail.com

🌐 https://github.com/your-username

🏁 Summary

Customer Behaviour Analysis showcases how Python and SQL can work together to automate data ingestion and enable deep business insights.
This project demonstrates strong skills in data engineering, database integration, and analytics — essential for real-world data science workflows.
