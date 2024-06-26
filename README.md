# PizzaSales

### Page 1: Business Overview
![Dashboard home](assets/images/Dashboard.png)
### Page 2: Sales Analysis
![Dashboard home](assets/images/dashboard_sales.png)


# Table of Contents
- [Objective](#objective)
- [Data Source](#data-source)
- [Stages](#stages)
  - [Tools](#tools)
  - [Development](#development)
  - [Pseudocode](#pseudocode)
  - [Data Cleaning](#data-cleaning)
- [Testing](#testing)
  - [Data Quality Checks](#data-quality-checks)
- [Visualisation](#visualisation)
  - [Results](#results)
  - [DAX Measures](#dax-measures)
- [Analysis](#analysis)
  - [Findings](#findings)
  - [Discovery](#discovery)

# Objective

* Key objectives for this project
The manager at this pizza shop wants to gain insights into how the business is performing, and he wants this information to be provided to him via an interactive dashboard. The dashboard should contain several key insights for the business, which will help him and his staff understand the data behind the business.

Ideal dashboard
The ideal dashboard should provide the relevant insights into the business, which includes key performance indicators such as;

  * The total revenue
  * Average Order value
  * Total pizzas sold
  * Total orders
  * Average pizzas per order
  
These KPIs will provide insightful information which the manager can use, furthermore, the dashboard should contain trends and insightful information, such as:

  * Total orders per day of the week
  * Total orders for hours of the day
  * Percentage of sales per pizza category
  * Percentage of sales per pizza size
  * Total sales per pizza
  * The top 5 best sellers by revenue
  * The bottom 5 sellers by total orders
  * The bottom 5 sellers by revenue
  * The bottom 5 sellers by total orders
  
The business can use this information to then make data driven decisions, such as, if it is worth continuing selling the bottom 5 popular pizzas.

# User story

As the manager of this pizza store, I want to identify key performance indicators and trends, such as the total revenue, total pizzas sold, the top 5 best sellers, the 5 lowest sellers, and several other insights. This is so I can make data driven decisions to help the business grow and generate more profit.

# Data Source

What data is needed to achieve the objectives?

* We need data on the pizza shop and their sales, such as:
** Pizza name
** Order date
** Quantity sold
** Total orders
** Total sales
** Pizza category
** Order time

# Stages

The stages for this project will be;
  * Design
  * Development
  * Testing
  * Analysis

# Stages

What should the dashboard contain?
To understand what the dashboard should contain, we need to figure out what questions we need the dashboard to answer, which will help provide the data to make data driven decisions. Some of the questions are as below:
* What day of the week has the highest number of orders?
* What hour of the day has the highest number of orders?
* Which category of pizza is the most popular?
* What are the top 5 pizzas by revenue?
* What are the bottom 5 pizzas by revenue?
* What are the top 5 pizzas by total orders?
* What are the bottom 5 pizzas by total orders?
* What is the percentage of sales per pizza category?
* What is the percentage of sales per pizza size?

## Tools

| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data |
| SQL Server | Cleaning, testing, and analysing the data |
| Power BI | Visualising the data via interactive dashboards |
| GitHub | Hosting the project documentation and version control |

# Development
## Pseudocode
What is the approach you will use to create a solution from start to finish?

1. Get the data
2. Explore the data using Microsoft Excel
3. Load the data into SQL
4. Clean the data with SQL
5. Test the data with SQL
6. Visualise the data in Power Bi
7. Generate the findings based on the insights
8. Write the documentation
9. Publish the data to GitHub


## Data Cleaning
  
  * What should the clean data look like?

The clean data should be structured and ready for analysis, and it should meet the following criteria and constraints:
 
1. Only relevant columns should be retained
2. All data types should be appropriate for the contents of each column
3. No NULL values in any of the columns
4. Correct data types for each column

Below is a table outlining the constraints on our cleaned data:

| Property | Description |
| --- | --- |
| Number of Rows | 48,620 |
| Number of Columns | 12 |

# Testing
Data quality and validation tests I conducted are as below:

## Row count check
### SQL Query
```sql
/*

-- 1. Row Count Check - Expected 46,620 (Passed)
SELECT
	COUNT(*) AS row_count
FROM pizza_sales;

```
### Output
![row_count_check](assets/images/row_count.png)

## Column count check
### SQL Query
```sql
/*

-- 2. Column Count Check - Expected 12 (Passed)
SELECT 
	COUNT(*) AS column_count
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'pizza_sales';

```
### Output
![row_count_check](assets/images/column_count.png)

## Data type check
### SQL Query
```sql
/*

SELECT 
	COLUMN_NAME,
	DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'pizza_sales';

```
### Output
![row_count_check](assets/images/data_type_check.png)

# Visualisation

## Results
The dashboard looks as below:
### Page 1: Business Overview
![Dashboard home](assets/images/Dashboard.png)
### Page 2: Sales Analysis
![Dashboard home](assets/images/dashboard_sales.png)

# Dax Measures

### 1. Total Revnue ($)
```sql
Total Revenue ($) = ROUND(SUM(pizza_sales[total_price]), 2)
```

### 2. Total Orders
```sql
Total Orders = DISTINCTCOUNT(pizza_sales[order_id])
```

### 3. Total Pizzas Sold
```sql
Total Pizzas Sold = SUM(pizza_sales[quantity])
```

### 4. AVG Order Value ($)
```sql
AVG Order Value ($) = ROUND(DIVIDE(SUM(pizza_sales[total_price]),
			DISTINCTCOUNT(pizza_sales[order_id])), 2)
```

### 5. AVG Pizzas Sold
```sql
AVG Pizzas Sold Per Order = ROUND(DIVIDE(SUM(pizza_sales[quantity]),
			    DISTINCTCOUNT(pizza_sales[order_id])), 2)
```

### 6. Sales Percentage Per Category
```sql
SalesPercentagePerCategory = 
DIVIDE(
    SUM(pizza_sales[total_price]),
    CALCULATE(SUM(pizza_sales[total_price]), ALL(pizza_sales[Pizza category]))
) * 100
```

### 7. Sales Percentage Per Size
```sql
SalesPercentagePerSize = 
DIVIDE(
    SUM(pizza_sales[total_price]),
    CALCULATE(SUM(pizza_sales[total_price]), ALL(pizza_sales[Pizza size]))
) * 100
```

# Analysis 

## Findings

* What were our findings?
There were several key questions we needed to answer for the pizza shop manager:

1. What day of the week has the highest number of orders?
2. What hour of the day has the highest number of orders?
3. Which category of pizza is the most popular?
4. What are the top 5 pizzas by revenue?
5. What are the bottom 5 pizzas by revenue?
6. What are the top 5 pizzas by total orders?
7. What are the bottom 5 pizzas by total orders?
8. What is the percentage of sales per pizza category?
9. What is the percentage of sales per pizza size?

### 1. What day of the week has the highest number of orders?
![days_of_week](assets/images/orders_per_day.png)

### 2. What hour of the day has the highest number of orders?
![orders_per_hour](assets/images/orders_per_hour.png)

### 3. Which category of pizza is the most popular?
![pizza_category](assets/images/total_sales_per_category.png)

### 4. What are the top 5 pizzas by revenue?
![pizza_category](assets/images/top5byrevenue.png)

### 5. What are the bottom 5 pizzas by revenue?
![pizza_revenue](assets/images/bottom5byrevenue.png)

### 6. What are the top 5 pizzas by total orders?
![top 5 by total orders](assets/images/top5pizzas.png)

### 7. What are the bottom 5 pizzas by total orders?
![bottom 5 by total orders](assets/images/bottom5pizzas.png)

### 8. What is the percentage of sales per pizza category?
![% per category](assets/images/pct_per_category.png)

### 9. What is the percentage of sales per pizza size?
![% per size](assets/images/pct_per_size.png)

## Discovery

* What did we learn?

We disovered that

1. Fridays are the busiest days as they have the most total orders (3,538), whereas, Sunday is the least busiest day as it has the least amount of total orders (2,624)
2. Lunch times (12:00 - 13:00) and dinner times (17:00 - 19:00) are the busiest times of the day, as they all had a total orders of over 2000
3. The classic category is the most popular with 14,888 pizzas sold in this category, whereas, chicken is the least popular with 11,050 of pizzas in this category sold
4. What the top 5 pizzas in terms of revenue are
5. What the bottom 5 pizzas in terms of revenue are, which can be useful to make data driven decisions
6. What the top 5 pizzas by total orders are
7. What the bottom 5 pizzas by total orders are, which can be useful to make data driven decisions
8. The percentage share per category of pizzas sold is quite balanced, as classic holds the highest percentage at 26.91%, and veggie holds the least percentage at 23.68%
9. Large and Medium size pizzas are the most popular, whereas, XXL and XL are the least popular

## Recommendations 

What do you recommend based on the insights gathered?

1. As we know Sundays are the least busiest days, we could offer discounts for pizzas on Sundays to increase the sales, which should then increase the revenue.
2. Lunch and Dinner times are the busiest times of the day, so we could offer discounts at other times of the day to increase sales during off peak hours
3. The chicken category has the least amount of pizzas sold, so I recommend we increase advertising and highlight the least popular pizza categories to increase visibility, which should then increase the total sum of orders and revenue
4. We know what the bottom 5 pizzas are in terms of revenue and total orders, so we can offer discounts on these pizzas, which should increase the demand for them. Furthermore, we can also gather customer feedback on these pizzas, to get their views on the pizza, what we could improve, and whether they would order them
5. We know that the XXL and XL Pizzas are the least popular, so we can offer discounts on the these sizes in hopes that the demand for them increases
