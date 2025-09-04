# Pizza-Sales-Analysis

## Table of Contents
-	[Tools](#tools)
-	[Data Cleaning and Preparation](#data-cleaning-and-preparation)
-	[Exploratory Data Analysis](#exploratory-data-analysis)
-	[Data Analysis](#data-analysis)
-	[Results and Findings](#results-and-findings)
-	[References](#references)


### Project Overview
This data analysis project aims to analyze Pizza Sales data to gain insights into customer behavior, sales trends, and product performance. Using data analysis techniques, I explored the dataset to identify key pizzas of sales, pattern in order time, and opportunities for business growth.
Tableau Dashboard
<img width="1375" height="765" alt="Screenshot 2025-09-04 101941" src="https://github.com/user-attachments/assets/279598f3-961a-461e-9349-df21d7beeccb" />

PowerBi Dashboard
<img width="1349" height="734" alt="Screenshot 2025-09-04 200542" src="https://github.com/user-attachments/assets/8a289f29-a951-4b9f-8629-4720fbf34c20" />

### Tools	
-	SQL Server
-	Excel
-	Tableau
-	PowerBi

### Data Cleaning and Preparation	
-	Data Archiving for recovery
-	Checked for duplicates
-	Standardize tables, checking for misspelled words and null values
  
### Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions, such as:
-	KPIs
o	Total Revenue
o	Average Oder Value
o	Total Pizzas Sold
o	Total Orders
o	Average Pizzas Per Order
-	Daily Trend for Total Orders
-	Hourly Trend for Orders
-	Percentage of Sales by Pizza Category
-	Percentage of Sales by Pizza Size
-	Total Pizzas sold by Pizza Category
-	Top 5 Best Sellers by Total Pizzas sold
-	Bottom 5 Best Sellers by Total Pizzas Sold
  
### Data Analysis
```sql
-- 1. TOTAL REVENUE
select sum(total_price) as total_revenue from pizza_sales2;

-- 2. AVERAGE ORDER VALUE
select sum(total_price) / count(distinct order_id) as avg_order_value from pizza_sales2;  

-- 3. TOTAL PIZZAS SOLD
select sum(quantity) as total_pizza_sold from pizza_sales2;

-- 4. TOTAL ORDERS
select count(distinct order_id) as total_orders from pizza_sales2;

-- 5. AVERAGE PIZZAS PER ORDER
select cast(sum(quantity) / count(distinct order_id) as decimal(10,2)) as avg_pizza_order 
from pizza_sales2;

-- 6. DAILY TREND FOR TOTAL ORDERS
select distinct order_day, count(distinct order_id) as total_orders from pizza_sales2
group by order_day order by total_orders desc;

-- 7. HOURLY TREND FOR ORDERS
select extract(hour from order_time) as order_hours, count(distinct pizza_id) as total_orders 
from pizza_sales2 group by order_hours 
order by order_hours;


-- 8. PERCENTAGE OF SALES BY PIZZA CATEGORY
select distinct pizza_category, cast(sum(total_price) as decimal(10,2)) as total_revenue, concat(cast(sum(total_price)*100 / 
(select sum(total_price) from pizza_sales2) as decimal(10,2)),'%') as PCT from pizza_sales2 
group by pizza_category order by PCT desc;

-- 9. PERCENTAGE OF SALES BY PIZZA SIZE
select distinct pizza_size, cast(sum(total_price) as decimal(10,2)) as total_revenue, concat(cast(sum(total_price)*100 / 
(select sum(total_price) from pizza_sales2) as decimal(10,2)),'%') as PCT from pizza_sales2 
group by pizza_size order by PCT desc;

-- 10. TOTAL PIZZAS SOLD BY PIZZA CATEGORY
select distinct pizza_category, sum(quantity) as sold_Pizza_by_cat
from pizza_sales2 group by pizza_category;

-- 11. TOP 5 BEST SELLERS BY TOTAL PIZZAS SOLD
select distinct pizza_name, sum(quantity)as total_pizza_sold from pizza_sales2
group by pizza_name order by total_pizza_sold desc limit 5;

-- 12 BOTTOM 5 BEST SELLERS BY TOTAL PIZZAS SOLD
select distinct pizza_name, sum(quantity)as total_pizza_sold from pizza_sales2
group by pizza_name order by total_pizza_sold asc limit 5;

```
### Results and Findings
1. Orders are high on weekends. Friday/Saturday evenings.
2. There are maximum orders from 12-01pm and after 04-08pm.
3. Classic Pizza Category and Large size pizza contributes to maximum sales and total orders.
4. Classic Deluxe Pizza is the best-selling pizza, and the Brie Carre Pizza is the least-selling pizza.
### References
-	[Stack Overflow] (https://stack.com)
