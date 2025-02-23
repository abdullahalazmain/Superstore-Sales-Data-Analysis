# Superstore Sales Data Analysis | RFM Segmentation

![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-Data_Cleaning-green)
![CSV-to-SQL](https://img.shields.io/badge/Rebasedata-CSV_to_SQL_Tool-orange)

This repository contains an end-to-end data analysis project using **Superstore Sales Data**. The project focuses on setting up a **MySQL** database, cleaning and transforming raw sales data, performing exploratory analysis **(EDA)**, and implementing **RFM (Recency, Frequency, Monetary) segmentation** to categorize customers based on their purchasing behavior.

---

## 📋 Overview

The goal of this project is to:
- Clean and format raw sales data.
- Convert the cleaned CSV to SQL.
- Create a database and table under that database.
- Import the SQL file into MySQL and perform exploratory analysis.
- Segment customers using **RFM (Recency, Frequency, Monetary)** analysis.

---

## 🚀 Features

- **Data Cleaning**: Handled blank cells, renamed columns, and fixed date formats in Google Sheets.
- **CSV-to-SQL Conversion**: Automated SQL schema creation and bulk insertion using Rebasedata.
- **RFM Segmentation**: SQL queries to classify customers into actionable groups (e.g., "Loyal Customers", "At-Risk").
- **Exploratory Analysis**: Analyzed sales trends, regional performance, and product profitability.

---

## 🛠️ Installation & Setup

### Prerequisites
- MySQL Workbench
- Google Sheets (or Excel) for data cleaning
- [Rebasedata](https://www.rebasedata.com/) (free CSV-to-SQL converter)

### Steps:

1. **Data Cleaning in Google Sheets**:
   - Open `superstore_raw.csv` in Google Sheets.
   - Perform cleaning:
     - Fill blank cells (e.g., using `CTRL + Click` or `Go To > Special > Blanks`).
     - Update column names for consistency (e.g., `Order ID` → `order_id`).
     - Fix date formats (e.g., `MM/DD/YYYY` → MySQL-friendly `YYYY-MM-DD`).
   - Export cleaned data as `superstore_clean.csv`.

2. **Convert CSV to SQL**:
   - Upload `superstore_clean.csv` to **[Rebasedata](https://www.rebasedata.com/)**.
   - Download the generated `.sql` file (includes table schema and data).
3. **Create Database in MySQL**:
   - If the `superstore` database doesn’t exist, create it first:  
  ```sql
  CREATE DATABASE superstore;
  ```
3. **Import SQL into MySQL**:
   - **Steps**:  
      1. **Connect to Server**:  
            Open MySQL Workbench and connect to your MySQL server.  

      2. **Open Data Import**:  
            Go to `Server` > `Data Import` in the top menu.  

      3. **Select Import Options**:  
          - Choose `Import from Self-Contained File`.  
         - Browse and select your `superstore_clean.sql` file.  
         - Under `Default Target Schema`, select or create the `superstore` database.  

      4. **Start Import**:  
            Click `Start Import` at the bottom-right.  
   
   ![MySQL Workbench Data Import Screenshot](https://i.imgur.com/abc123.png) *(Optional: Add a screenshot if available)*  

      **Why Use This?**  
      - **Beginner-Friendly**: No command-line commands required.  
      - **Progress Tracking**: Visual progress bar for large files.  
      - **Error Logging**: Detailed error messages if the import fails.  

5. **Run Analysis Queries**:
   - Use MySQL Workbench or CLI to execute RFM segmentation and EDA queries (examples below).

---

### Another Way:
1. **Database Setup**: Created a MySQL database and table schema tailored for the Superstore dataset.
2. **Bulk Data Insertion**: Efficiently imported the dataset into MySQL using `Table Data Import Wizard` or `LOAD DATA INFILE`.
3. **Data Cleaning & Validation**:  
   - Standardized date formats.  
   - Handled missing/duplicate values.  
   - Ensured consistent data types (e.g., sales, profit as `DECIMAL`, dates as `DATE`).  
   - Updated table schema for optimization (e.g., indexing, constraints).  
4. **Exploratory Data Analysis (EDA)**:  
   - Analyzed sales trends, regional performance, and product category insights.  
   - Identified top customers and profitable products.  
5. **RFM Customer Segmentation**:  
   - Calculated **Recency**, **Frequency**, and **Monetary Value** metrics.  
   - Segmented customers into groups (e.g., "High-Value", "At-Risk", "Champions") for targeted strategies.

---

## ❓ Why Google Sheets & Rebasedata?

I chose **Google Sheets** and **Rebasedata** for data cleaning and SQL conversion due to challenges faced with direct CSV imports in MySQL:

### Issues with Direct MySQL CSV Import:
1. **Formatting Errors**:  
   MySQL often failed to parse dates, strings with special characters (e.g., `'` in names), or numeric fields with inconsistencies (e.g., `$1,000` as text).
2. **Data Loss**:  
   Columns with mixed data types (e.g., postal codes stored as numbers) caused incomplete imports or truncated values.
3. **Time-Consuming Fixes**:  
   Manually editing schemas, handling missing values, and debugging import errors took hours.
4. **Bulk Insertion Failures**:  
   Large datasets (e.g., 10,000+ rows) frequently caused timeouts or incomplete imports.

### How Google Sheets & Rebasedata Solved These:
- **Google Sheets**:  
  - ✅ **Visual Data Cleaning**: Easily fill blank cells, rename columns, and fix date formats without coding.  
  - ✅ **Prevent Data Loss**: Ensure consistency (e.g., postal codes as text, sales as numbers) before conversion.  
  - ✅ **User-Friendly**: No SQL expertise needed for initial cleanup.  

- **Rebasedata**:  
  - ✅ **Automated Schema Generation**: Converts CSV columns to correct MySQL data types (e.g., `DATE`, `DECIMAL`).  
  - ✅ **Bulk Insertion Made Easy**: Generates optimized `.sql` files for seamless imports, avoiding timeouts.  
  - ✅ **Error-Free**: Handles special characters, quotes, and formatting issues automatically.  

### The Result:  
A streamlined workflow that saved time, reduced errors, and ensured **100% data integrity** during migration.  

---

**❓ Why This Project?**  
This project demonstrates skills in **database management**, **data wrangling**, and **customer behavior analysis**. It provides a template for handling real-world sales data and actionable insights through RFM segmentation.  
  
--- 

## 📊 Usage

### Example Queries

1. **RFM Segmentation**:
   ```sql
   WITH rfm AS (
       SELECT
           customer_id,
           DATEDIFF(CURDATE(), MAX(order_date)) AS recency,
           COUNT(order_id) AS frequency,
           SUM(sales) AS monetary
       FROM sales
       GROUP BY customer_id
   )
   SELECT
       customer_id,
       recency,
       frequency,
       monetary,
       CASE
           WHEN recency < 30 AND frequency > 5 AND monetary > 1000 THEN 'Champions'
           WHEN recency > 365 THEN 'Inactive'
           ELSE 'Needs Attention'
       END AS rfm_segment
   FROM rfm;
   ```

2. **Sales by Region**:
   ```sql
   SELECT region, SUM(sales) AS total_sales
   FROM sales
   GROUP BY region
   ORDER BY total_sales DESC;
   ```

---

## 🛠️ Tools Used
- **Data Cleaning**: Google Sheets
- **CSV-to-SQL Conversion**: [Rebasedata](https://www.rebasedata.com/)
- **Database**: MySQL
- **Analysis**: Pure SQL queries

---

## 📄 License

MIT License. See [LICENSE](LICENSE) for details.

---

## 🙏 Credits

- Tool: [MySQL](https://www.mysql.com/) for Data analysis.
- Tool: [Google Sheets](https://workspace.google.com/products/sheets/) for data cleaning.
- Tool: [Rebasedata](https://www.rebasedata.com/) for CSV-to-SQL conversion.

