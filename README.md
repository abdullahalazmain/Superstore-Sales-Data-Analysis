# Superstore-Sales-Data-Analysislaisis
"Explore Superstore sales data with MySQL database setup, bulk data insertion, and cleaning. Perform EDA and RFM customer segmentation using Excel &amp; SQL. #DataAnalysis #CustomerSegmentation #MySQL #EDA"
Superstore Sales Data Analysis | RFM Segmentation
MySQL
Google Sheets
CSV-to-SQL

This project analyzes Superstore Sales Data to segment customers using RFM analysis. The workflow includes data cleaning in Google Sheets, converting CSV to SQL using Rebasedata, and performing analysis directly in MySQL.

📋 Overview
The goal of this project is to:

Clean and format raw sales data using Google Sheets.

Convert the cleaned CSV to SQL using Rebasedata.

Import the SQL file into MySQL and perform exploratory analysis.

Segment customers using RFM (Recency, Frequency, Monetary) analysis.

🚀 Features
Data Cleaning: Handled blank cells, renamed columns, and fixed date formats in Google Sheets.

CSV-to-SQL Conversion: Automated SQL schema creation and bulk insertion using Rebasedata.

RFM Segmentation: SQL queries to classify customers into actionable groups (e.g., "Loyal Customers", "At-Risk").

Exploratory Analysis: Analyzed sales trends, regional performance, and product profitability.

🛠️ Installation & Setup
Prerequisites
MySQL Server

Google Sheets (or Excel) for data cleaning

Rebasedata (free CSV-to-SQL converter)

Steps:
Clone the repository:

bash
Copy
git clone https://github.com/your-username/superstore-sales-analysis.git
cd superstore-sales-analysis
Data Cleaning in Google Sheets:

Open superstore_raw.csv in Google Sheets.

Perform cleaning:

Fill blank cells (e.g., using CTRL + Click or Go To > Special > Blanks).

Update column names for consistency (e.g., Order ID → order_id).

Fix date formats (e.g., MM/DD/YYYY → MySQL-friendly YYYY-MM-DD).

Export cleaned data as superstore_clean.csv.

Convert CSV to SQL:

Upload superstore_clean.csv to Rebasedata.

Download the generated .sql file (includes table schema and data).

Import SQL into MySQL:

sql
Copy
-- Run the generated SQL file in MySQL
mysql -u your_username -p superstore < superstore_clean.sql
Run Analysis Queries:

Use MySQL Workbench or CLI to execute RFM segmentation and EDA queries (examples below).

