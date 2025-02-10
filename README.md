# Project : Sales Insights Dashboard using PowerBI
 <u></u> 

## Problem Statement :
 <u></u>
AtliQ Hardware company sales insights - A Data Analysis project.

AtliQ Hardware is a company which supplies computer hardwares and peripherals across India having head office in delhi and many regional offices through out India. Sales director of this company is facing a lot of challenges with decline in sales in dynamically growing market. He is unable to track the sales in real time and take data driven decision to rectify the decline in sales. He is not getting satisfactory report or insights from regional managers of different zones. Reports are not in simpler form instead lots of excel files which are hard to get clear insights.

## Solution :
 <u></u>

Sales Director of the AltiQ hardware decided to have a Sales Insights Dashboard to get insights in simpler form in realtime and take data driven decision to increase sales of the company.

## Steps to be Followed in this project
<u></u>
1. Learned about AIMS grid for project planning.
2. Imported db_dump.sql file in MySQL and performed Data Analysis Using SQL.
3. Used MySQL for retrieving the data from the database into Power BI.
4. Data Cleaning in power query and ETL (Extract, Transform, Load)
5. Exploratory Data Analysis(EDA)
6. Data Modeling and DAX
7. Data Visualization.

## AIMS Grid :
 <u></u>
 AIMS grid project management tool is being used here which consists of four components.
 
![AIMS grid sales insights](https://github.com/user-attachments/assets/a17b8db5-ad7e-427c-864e-849c86bad919)

## Data Analysis using MySQL :
<u></u>
1. Show all customer records
       SELECT * FROM customers;
2. Show total number of customers
       SELECT count(*) FROM customers;
3. Show transactions for Chennai market (market code for chennai is Mark001
       SELECT * FROM transactions where market_code='Mark001';
4. Show distrinct product codes that were sold in chennai
       SELECT distinct product_code FROM transactions where market_code='Mark001';
5. Show transactions where currency is US dollars
       SELECT * from transactions where currency="USD"
6. Show transactions in 2020 join by date table
       SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
7. Show total revenue in year 2020,
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR" or 
       transactions.currency="USD";
8. Show total revenue in year 2020, January Month,
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and date.month_name="January" and 
       (transactions.currency="INR" or transactions.currency="USD");
9. Show total revenue in year 2020 in Chennai
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
       and transactions.market_code="Mark001";

## Data Cleaning and ETL (Extract, Transform, Load):
<u></u>
In this process, we are work on data cleaning and ETL.

Step 1: Connect the MySQL database with the PowerBI desktop.

Step 2: Loading data into the Power BI deskstop. This step load all the tables and created in the data base. This load option will connect with the SQL and pull all the records into 
        power BI environment.
        
Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using  formulas  and remove cities like Paris, New York not having zone.    
In power query editor ->  = Table.SelectRows(sales_markets, each ([zone] <> ""))
                          = Table.AddColumn(sales_transactions, "norm_sales_amount", each if [currency] = "USD" then [sales_amount]*75 else[sales_amount])
