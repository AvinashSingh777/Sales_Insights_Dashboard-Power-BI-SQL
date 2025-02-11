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

1. Show all customer records <br />
       SELECT * FROM customers;
2. Show total number of customers <br />
       SELECT count(*) FROM customers;
3. Show transactions for Chennai market (market code for chennai is Mark001 <br />
       SELECT * FROM transactions where market_code='Mark001';
4. Show distrinct product codes that were sold in chennai <br />
       SELECT distinct product_code FROM transactions where market_code='Mark001';
5. Show transactions where currency is US dollars <br />
       SELECT * from transactions where currency="USD"
6. Show transactions in 2020 join by date table <br />
       SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
7. Show total revenue in year 2020, <br />
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR" or 
       transactions.currency="USD";
8. Show total revenue in year 2020, January Month, <br />
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and date.month_name="January" and 
       (transactions.currency="INR" or transactions.currency="USD");
9. Show total revenue in year 2020 in Chennai <br />
       SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
       and transactions.market_code="Mark001";


## Data Cleaning and ETL (Extract, Transform, Load):
<u></u>

In this process, we are work on data cleaning and ETL.

Step 1: Connect the MySQL database with the PowerBI desktop.

Step 2: Loading data into the Power BI deskstop. This step load all the tables and created in the data base. This load option will connect with the SQL and pull all the records into 
        power BI environment.
        
Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using  formulas  and remove cities like Paris, New York not having zone.

In power query editor -> 1. = Table.SelectRows(sales_markets, each ([zone] <> ""))
                         2. = Table.AddColumn(sales_transactions, "norm_sales_amount", each if [currency] = "USD" then [sales_amount]*75 else[sales_amount])


## Data Modeling and DAX :
<u></u>

Dataset was cleaned and transformed, it was ready for the data modeling.
The sales insights data tables as show below:

![Data_Model](https://github.com/user-attachments/assets/ce2eccbc-791d-4196-9d4f-58340cf4b8c6)

## Key Measures :

1. Profit Margin % = DIVIDE([Total Profit Margin],[Revenue],0)
2. Profit Margin Contribution % = DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('sales products'),ALL('sales 
   customers'),ALL('sales markets')))
3. Revenue = SUM('sales transactions'[sales_amount])
4. Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))
5. Revenue LY = CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))
6. sales quntity = SUM('sales transactions'[sales_qty])
7. Total Profit Margin = SUM('Sales transactions'[Profit_Margin])


## Data Visualization :


Dashboard - Key Insights
<u></u>

![DashBoard_1](https://github.com/user-attachments/assets/d6a56c65-9f11-44ad-a402-2f3e9aa00f0f)

<u></u>

Dashboard - Profit Analysis
<u></u>

![Dashboard_2 1](https://github.com/user-attachments/assets/a524d160-6c67-4da1-99c4-69835500e984)



Dashboard - Profit Analysis(2020)
<u></u>

![Dashboard_2 2](https://github.com/user-attachments/assets/c149ab23-5a30-439b-8e2f-961c453b3d43)

<u></u>


Dashboard - Performance Insights(2020)
<u></u>

![DashBoard_PerformanceInsights](https://github.com/user-attachments/assets/8d4c7b11-fd9d-4eff-a5c0-1f08a486c57f)


## Insights
<u></u>

1. In this dashboard, we can see company has generated total revenue in 4 years ₹ 985M, total profit margin ₹24.7M, Profit margin% 2.5%, Sales Qty ₹2M. in 2020 company has generated total revenue of ₹ 142M by selling a total of 350K and earned a profit of ₹ 2.1M.
2. In 4 years Delhi NCR is our largest market in terms of revenue with ₹ 520M and total contribution of 52.8% with total revenue but if you look at the profit margin Delhi NCR is generating only 2.3% profit margin.
3. If we check the profit margin then here In 2020 Bhubaneshwar comes into the picture which is generating the highest profit margin of 10.48%. Similarly, if we can check the Profit Contribution % by Market then here Mumbai is the largest player with 23.89% of total contribution in total profit.
4. In 4 years Bengaluru generating the lowest profit margin of -20.8%.if we can check the Profit Contribution % by Market then here also Bengaluru is the Lower with -0.3% of total contribution in total profit.
5. In our top 5 customers, the Electricalsara Stores is our biggest customer who has generated total ₹ 413 M revenue generated in 4 years.
6. In our top 5 products, highest product has generated total ₹ 469M revenue generated in 4 years.
7. Revenue Trend is showing that in June 2020 revenue has been decreased drastically compared to the revenue last year and the profit margin was the least in April 2020.
