# Retail chain
Data Cleaning and Quality Check for Retail Chain Dataset SQL-based data cleaning project using MySQL. Tasks include schema setup, data import, missing value checks, duplicate detection, and validation of product and sales data.
## Table of Contents
- [Overview](Overview)
- [Tools Used](Tools-Used)
- [Step-by-Step Process](Step-by-Step-Process)
- [Summary of Results](Summary-of-Results)
- [Conclusion](Conclusion)
## Overview
This project demonstrates the process of **data cleaning and validation** using SQL in MySQL Workbench.  
The dataset consists of two tables  `product_table` and `sales_table` both stored under the `retail_chain` schema.  
The goal is to identify and fix data quality issues such as missing values, duplicates, and invalid entries.

## Tools Used
- MySQL Workbench
- CSV Data Files - Products and Sales [Download here](https://drive.google.com/drive/folders/1C54PD3F7tclg7XNUXuvosH_leBDD8StO)
- GitHub - for documentation and submission

## Step-by-Step Process

### Step 1: Create a New Schema
Query
```sql
CREATE SCHEMA RETAIL_CHAIN;
```
### STEP 2: Select Database
```sql
USE RETAIL_CHAIN;
```
### Step 3: Rename Tables for Consistency
Renamed both tables to remove spaces in their names.
Using underscores (_) ensures smooth querying and better code readability.
```sql
RENAME TABLE `PRODUCT TABLE` TO PRODUCT_TABLE;
RENAME TABLE `SALES TABLE` TO SALES_TABLE;
```
### Step 4: Viewed Table Data
Previewed both tables to understand their structure and data contents.
```sql
SELECT * FROM PRODUCT_TABLE;
SELECT * FROM SALES_TABLE;
```
### Step 5: Inspect Data Table Structures
Displayed column names, data types, and constraints to guide cleaning and validation steps.
```sql
DESCRIBE PRODUCT_TABLE;
DESCRIBE SALES_TABLE;
```
### Step 6: Check for Missing Values
Checked for null values in important numeric columns.
```sql
SELECT COUNT(*) FROM PRODUCT_TABLE WHERE UNIT_PRICE IS NULL;
SELECT COUNT(*) FROM PRODUCT_TABLE WHERE STOCK_QUANTITY IS NULL;
SELECT COUNT(*) FROM SALES_TABLE WHERE QUANTITY IS NULL;
```
### Step 7: Check for Duplicates
This checks if any PRODUCT_ID appears more than once in the sales_table.
```sql
SELECT PRODUCT_ID, COUNT(*) AS OCCURENCE
FROM SALES_TABLE
GROUP BY PRODUCT_ID
HAVING COUNT(*) > 1;
```
### Step 8: Check for Invalid or Negative Quantities
Ensures all quantities sold are positive.
```sql
SELECT *
FROM SALES_TABLE
WHERE QUANTITY <= 0;
```
### Step 9: Check for Outliers
Verified that price and quantity values are within reasonable ranges.
#### Result
UNIT_PRICE: Minimum = 0.65, Maximum = 5.20
QUANTITY: Minimum = 1, Maximum = 5
No unrealistic or extreme values observed.
```sql
SELECT MIN(UNIT_PRICE) AS MIN_PRICE, MAX(UNIT_PRICE) AS MAX_PRICE
FROM PRODUCT_TABLE;

SELECT MIN(QUANTITY) AS MIN_QUANTITY, MAX(QUANTITY) AS MAX_QUANTITY
FROM SALES_TABLE;
```
### Summary of Results
- No missing data.
- No duplicate product IDs.
- No invalid or unrealistic values.
- Data is clean and ready for further analysis.

### Conclusion
Both tables in the retail_chain database are clean, complete, and ready for analysis.



