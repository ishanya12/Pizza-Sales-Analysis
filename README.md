# Pizza-Sales-Analysis

## Table of Contents

•	Problem Statement

•	Dataset Overview

•	Data Analysis using MySQL

•	Key Feature of Dashboard

•	Key Insights and Findings

•	Challenges Faced 

•	Tools and Software
________________________________________
## Problem Statement
The objective of this project is to analyze pizza sales data to identify key sales trends, customer preferences, and inventory management. The primary goals include :

•	Understanding revenue trends over time.

•	Identifying the best-selling and least-selling pizza types.

•	Analyzing peak sales hour and order patterns.

•	Evaluating sales performance by pizza size and category.
________________________________________
## Dataset Overview
The dataset used for this includes transactional data from a pizza restaurant containing :

•	order_datails_id

•	order_id

•	pizza_id

•	quantity

•	order_date

•	order_time

•	unit_price

•	total_price

•	pizza_size

•	pizza_category

•	pizza_ingredients

•	pizza_name
This dataset allows us to derive meaningful insights related to sales trends, demand forecasting, and customer behavior.
________________________________________
## Data Analysis using MySQL
Steps Involved :
1.	Importing and cleaning the dataset.
2.	Exploring key sales metrics such as revenue, best-selling pizzas, and peak sales hours.
3.	Identifying customer preferences and demand patterns.
4.	Generating SQL queries to extract insights : 
	Total revenue.
	Best and worst-performing pizzas.
	Average order value.
	Peak order times.
	Sales contribution by pizza category.
SQL Queries :
--Total Quanity
``` sql
select SUM(quantity) as total_quantity from [Data Model];
```
--Total Order
 ```sql
select COUNT(distinct order_id) as total_order from [Data Model];
```
--Total Revenue
```sql
 select cast (SUM(total_price)  as decimal(10,4)) as total_income from [Data Model];
```
--Average order value
 ```sql
select cast (AVG (distinct total_price) as decimal(10,2)) as average  from [Data Model];
```
--Average pizza per order
```sql
 select sum(quantity) / count(distinct order_id) as average_per_order from [Data Model];
```
--Daily Trends for Total Orders
 ```sql
select 
DATENAME(weekday, order_date) as day_name,
COUNT(order_id) as total_order
from [Data Model]
group by DATENAME(weekday,order_date)
order by
case 
when DATENAME(weekday, order_date) = 'Monday' then 1
when DATENAME(weekday, order_date) = 'Tuesday' then 2
when DATENAME(weekday, order_date) = 'Wednesday' then 3
when DATENAME(weekday, order_date) = 'Thursday' then 4
when DATENAME(weekday, order_date) = 'Friday' then 5
when DATENAME(weekday, order_date) = 'Saturday' then 6
when DATENAME(weekday, order_date) = 'Sunday' then 7
end;
```
--Monthly Trends for Orders
 ```sql
select 
MONTH(order_date) as month,
COUNT(order_date) as total_orders,
SUM(quantity) as total_quantity,
SUM(total_price) as total_sales
from [Data Model]
group by 
MONTH(order_date)
order by 
month desc;
```
--Percentage Sale by Pizza Category
 ```sql
select
pizza_category ,
SUM(total_price) as category_sales,
round ((SUM(total_price) / (select SUM(total_price) from [Data Model]) * 100), 2) as percentage
from [Data Model]
group by pizza_category
order by percentage desc;
```
--Percentage Sale by Pizza Size
 ```sql
select
pizza_size ,
SUM(total_price) as size_sales,
round ((SUM(total_price) / (select SUM(total_price) from [Data Model]) * 100), 2) as percentage
from [Data Model]
group by pizza_size
order by percentage desc;
```
--Total Sold by Category
 ```sql
select
pizza_category,
SUM(quantity) as total_sale
from [Data Model]
group by pizza_category
order by total_sale desc;
```
--Top 5 Pizza by Revenue
 ```sql
select top 5
pizza_name,
SUM(total_price) as total_revenue
from [Data Model]
group by pizza_name
order by total_revenue desc;
```
--Bottom 5 Pizza by Revenue
 ```sql
select top 5
pizza_name,
SUM(total_price) as total_revenue
from [Data Model]
group by pizza_name
order by total_revenue asc
```
--Top 5 by Orders
 ```sql
select top 5
pizza_name,
SUM(order_id) as total_order
from [Data Model]
group by pizza_name
order by total_order desc;
```
--Bottom 5 by Orders
 ```sql
select top 5
pizza_name,
SUM(order_id) as total_order
from [Data Model]
group by pizza_name
order by total_order asc;
```
--Top 5 by Quantity
 ```sql
select top 5
pizza_name,
SUM(quantity) as total_quantity
from [Data Model]
group by pizza_name
order by total_quantity desc;
```
--Bottom 5 by Quantity
```sql
 select top 5
pizza_name,
SUM(quantity) as total_quantity
from [Data Model]
group by pizza_name
order by total_quantity asc;
```
 
________________________________________

## Key Features of the Dashboard :

•	Interactive filters for data range selection.

•	Drill-down options for specific categories.

•	Visual representation of revenue.
________________________________________
## Challenges Faced
•	Data Cleaning Issues: Handling missing timestamps and duplicate entries required preprocessing before analysis.

•	SQL Query Optimization: Running large queries on the dataset took longer than expected, requiring indexing and optimization.

•	Dashboard Performance: Ensuring the Power BI dashboard loads quickly with large datasets was a challenges that required optimizing extracts. 
________________________________________
## Tools and Software

•	Excel – Data Cleaning.

•	MySQL – Data extraction and analysis.

•	Power BI – Dashboard/report visualization.
________________________________________




