# Sales Insights Data Analysis Project
This project demonstrates an end-to-end data analytics workflow using SQL Server, MySQL Workbench, and Power BI for a retail sales dataset. You can follow the given instructions given below to clean, transform, and analyz through SQL and visualize in Power BI for your own practice. Key performance indicators (KPIs) like revenue, sales quantity, top customers, and regions were presented to derive insights. Originally derived from Codebasics Github. 

## 1. INSTALL SQL SERVER AND WORKBENCH 
## 2. DOWNLOAD THE db_dump.sql FILE ONTO YOUR LOCAL COMPUTER AND IMPORT INTO SQL 
## 3. Do some Data Exploration and understand your dataset by writing SQL Queries for the following:

NOTE: You don’t have to do “sales.” Everywhere if you right click on sales and set it as the default schema

- Show all transactions
- Show all currencies in usd
- What is the total number of sales transactions?
- What is the total number of customers?
- Show all markets
- Show all the transactions from chennai
- How many transactions were performed in chennai
- Show the total revenue (business) you did in chennai
- Inner join the date and transaction table using the year column
- Then show all the transactions that were made in the year 2020
- Show the total revenue in 2020
- Show the total revenue in 2020 in chennai
- Show all the distinct products sold in chennai
- Check if the sales_amount column has negative or zero values in the transactions table
- Turns out there are duplicate currencies and we don’t want that so check the currency column in the transactions table and tackle this by deleting the bad/duplicate records for both currencies
- Show the total revenue in year 2020 by month january

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

- Show the total revenue in a card format using the using the norm_sales_amount column we created
- Show the total sales qty in a card format 
- Show The Total Revenue By Customer In A Horizontal Bar Chart Format
- Show The Total Sales Qty By Customer In A Horizontal Bar Chart Format
- Show The Years As A Slicer In Horizontal Orientation So You Can See The Revenue And Sales Qty By Year
- Show The Revenue And Sales Qty By Months, You’ll Have To Change The Formatting Of Cy_Date For This
- Verify / Cross Check In MySQL
- Show Revenue & Sales Qty Based On Market Name (So Regions) Instead Of Customer Name
- Show The Top 5 Customers As They Are Giving Me The Most Amount Of Business / Revenue, Change Title, Make Sure Customer Name Is Visible
- Show Which Top 5 Products Are Giving You The Most Amount Of Revenue
- Show A Line Chart For The Revenue Over By Cy Date, Change The Colour To Red, Get Rid Of The X & Y-Axis Labels
- What Are My Worst Performing Products?
- What Are The Worst Performing Regions?

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
  
