# Sales Insights Data Analysis Project
This project demonstrates an end-to-end data analytics workflow using SQL Server, MySQL Workbench, and Power BI for a retail sales dataset. You can follow the given instructions given below to clean, transform, and analyz through SQL and visualize in Power BI for your own practice. Key performance indicators (KPIs) like revenue, sales quantity, top customers, and regions were presented to derive insights. Originally derived from Codebasics Github. 

## 1. INSTALL SQL SERVER AND WORKBENCH 
## 2. DOWNLOAD THE db_dump.sql FILE ONTO YOUR LOCAL COMPUTER AND IMPORT INTO SQL 
## 3. Do some Data Exploration and understand your dataset by writing SQL Queries for the following:

NOTE: You don’t have to do “sales.” Everywhere if you right click on sales and set it as the default schema

- SHOW ALL TRANSACTIONS
- SHOW ALL CURRENCIES IN USD 
- WHAT IS THE TOTAL NUMBER OF SALES TRANSACTIONS? 
- WHAT IS THE TOTAL NUMBER OF CUSTOMERS? 
- SHOW ALL MARKETS
- SHOW ALL THE TRANSACTIONS FROM CHENNAI 
- HOW MANY TRANSACTIONS WERE PERFORMED IN CHENNAI
- SHOW THE TOTAL REVENUE (BUSINESS) YOU DID IN CHENNAI
- INNER JOIN THE DATE AND TRANSACTION TABLE USING THE YEAR COLUMN
- THEN SHOW ALL THE TRANSACTIONS THAT WERE MADE IN THE YEAR 2020
- SHOW THE TOTAL REVENUE IN 2020 
- SHOW THE TOTAL REVENUE IN 2020 IN CHENNAI
- SHOW ALL THE DISTINCT PRODUCTS SOLD IN CHENNAI
- CHECK IF THE SALES_AMOUNT COLUMN HAS NEGATIVE OR ZERO VALUES IN THE TRANSACTIONS TABLE
- TURNS OUT THERE ARE DUPLICATE CURRENCIES AND WE DON’T WANT THAT SO CHECK THE CURRENCY COLUMN IN THE TRANSACTIONS TABLE AND TACKLE THIS BY DELETING THE BAD/DUPLICATE RECORDS FOR BOTH CURRENCIES 
- SHOW THE TOTAL REVENUE IN YEAR 2020 BY MONTH JANUARY

## 4. Here are my answers for step 3 above: 

- SHOW ALL TRANSACTIONS
```sql
SELECT * FROM transactions;
```

- SHOW ALL CURRENCIES IN USD
```sql
SELECT * FROM transactions WHERE currency = 'USD';
```

- WHAT IS THE TOTAL NUMBER OF SALES TRANSACTIONS?
```sql
SELECT COUNT(*) FROM transactions;
```

- WHAT IS THE TOTAL NUMBER OF CUSTOMERS? 
```sql
SELECT COUNT(*) FROM customers;
```

- SHOW ALL MARKETS
```sql
SELECT * FROM markets;
```

- SHOW ALL THE TRANSACTIONS FROM CHENNAI 
```sql
SELECT * FROM transactions WHERE market_code = 'Mark001';
```

- HOW MANY TRANSACTIONS WERE PERFORMED IN CHENNAI 
```sql
SELECT COUNT(*) FROM transactions WHERE market_code = 'Mark001';
```

- SHOW THE TOTAL REVENUE (BUSINESS) YOU DID IN CHENNAI
```sql
SELECT SUM(sales_amount) FROM transactions WHERE market_code='Mark001';
```

- INNER JOIN THE DATE AND TRANSACTION TABLE USING THE YEAR COLUMN THEN SHOW ALL THE TRANSACTIONS THAT WERE MADE IN THE YEAR 2020
```sql
SELECT transactions.*, date.*
FROM transactions INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year=2020;
```

- SHOW THE TOTAL REVENUE IN 2020
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year=2020;
```

- SHOW THE TOTAL REVENUE IN 2020 IN CHENNAI
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year=2020 AND transactions.market_code='Mark001';
```

- SHOW ALL THE DISTINCT PRODUCTS SOLD IN CHENNAI
```sql
SELECT DISTINCT(transactions.product_code)
FROM transactions
WHERE transactions.market_code='Mark001';
```


- CHECK IF THE SALES_AMOUNT COLUMN HAS NEGATIVE OR ZERO VALUES IN THE TRANSACTIONS TABLE
```sql
SELECT *
FROM transactions
WHERE transactions.sales_amount<=0;
```


- TURNS OUT THERE ARE DUPLICATE CURRENCIES AND WE DON’T WANT THAT SO CHECK THE CURRENCY COLUMN IN THE TRANSACTIONS TABLE AND TACKLE THIS BY DELETING THE BAD/DUPLICATE RECORDS FOR BOTH CURRENCIES: 
```sql
SELECT distinct(transactions.currency) FROM transactions;
SELECT COUNT(*) FROM transactions.currency=’INR\r;
SELECT COUNT(*) FROM transactions.currency=’INR;
SELECT COUNT(*) FROM transactions.currency=’USD\r’ OR transactions.currency=’USD’ ;
```

- SHOW THE TOTAL REVENUE IN YEAR 2020 BY MONTH JANUARY
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions INNER JOIN date
ON transactions.order_date = date.date
WHERE date.year=2020 AND date.month_name=”January” AND (transactions.currency="INR\r" or transactions.currency="USD\r") ;
```

## 5. INSTALL POWER BI FROM THE MICROSOFT STORE
## 6. GET DATA IN POWER BI from your mySQL Database
## 7. ETL - EXTRACT TRANSFORM AND LOAD 
- Transform the zone column in the markets table to get rid of any zone rows with blank values
- THE SALES_AMOUNT CANNOT BE NEGATIVE or 0 SO CLEAN UP THAT COLUMN IN THE TRANSACTIONS TABLE by filtering them out
- CONVERT USD TO INR IN THE TRANSACTIONS TABLE - CURRENCY COLUMN. To do this you want to add a new column that is called a normalized_currency = this column will have all the converted sales amount in INR
- As noticed during the Data exploration phase in SQL - that we have duplicate currencies in the currency column - We are going to keep the records with USD\r and INR\r because most of the records have this value. 

NOTE: in real life you would have a spot_conversion_table which will have the currency conversion rates and you would use that to convert from usd to inr instead of 75 Because the currency conversion rates change constantly but for simplicity we are keeping it this way. 

## 8. SHOW THE FOLLOWING IN YOUR POWER BI REPORT:

NOTE: FILE OPTION+SETTINGS -> REPORT SETTINGS -> SELECT THE OPTION TO “CHANGE DEFAULT VISUAL INTERACTION FROM CROSS HIGHLIGHTING TO CROSS FILTERING” 

- SHOW THE TOTAL REVENUE IN A CARD FORMAT using the norm_sales_amount! 
- SHOW THE TOTAL SALES QTY IN A CARD FORMAT
- SHOW THE TOTAL REVENUE BY CUSTOMER IN A HORIZONTAL BAR CHART FORMAT
- SHOW THE TOTAL  SALES QTY BY CUSTOMER IN A HORIZONTAL BAR CHART FORMAT
- SHOW THE YEARS AS A SLICER IN HORIZONTAL ORIENTATION SO YOU CAN SEE THE REVENUE AND SALES QTY BY YEAR
- SHOW THE REVENUE AND SALES QTY BY MONTHS, YOU’LL HAVE TO CHANGE THE FORMATTING OF CY_DATE FOR THIS
- VERIFY / CROSS CHECK IN MYSQL
- SHOW REVENUE & SALES QTY BASED ON MARKET NAME (SO REGIONS) INSTEAD OF CUSTOMER NAME
- SHOW THE TOP 5 CUSTOMERS AS THEY ARE GIVING ME THE MOST AMOUNT OF BUSINESS / REVENUE, CHANGE TITLE, MAKE SURE CUSTOMER NAME IS VISIBLE
- SHOW WHICH TOP 5 PRODUCTS ARE GIVING YOU THE MOST AMOUNT OF REVENUE
- SHOW A LINE CHART FOR THE REVENUE OVER BY CY DATE, CHANGE THE COLOUR TO RED, GET RID OF THE X & Y-AXIS LABELS
- WHAT ARE MY WORST PERFORMING PRODUCTS?
- WHAT ARE THE WORST PERFORMING REGIONS? 

## 9. PUBLISH TO WEBSITE AND MOBILE APP: 
HERE YOU WILL NEED A WORK ACCOUNT
YOU CAN BOOKMARK STUFF
PEOPLE MIGHT COMMENT GIVING YOU FEEDBACK AND ASK YOU TO CHANGE STUFF
YOU CAN USE IT LIKE A PPT

Note: IN REAL LIFE YOU WOULD HAVE TO SCHEDULE A REFRESH TIME FOR MAKING YOUR REPORT REFLECT THE UPDATED DATABASE (SO IT WOULD CAPTURE THE LATEST DATA/TRANSACTIONS) - THIS WOULD REQUIRE YOU TO SET UP A GATEWAY CONNECTION

NOTE: You’ll have to change the layout to look good on your mobile. You can do this by clicking on the mobile layout option. 

## 10. UPDATE TO THE new correct database for better insights:
Update to the new sql_dump_ver2 data and then show the % of more profit margin
ROI = return on investment
Revenue contribution % =
Profit contribution % = 
Ideally you want the profit to be proportional to the revenue 
  
