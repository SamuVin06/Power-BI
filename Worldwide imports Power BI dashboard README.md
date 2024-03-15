# Worldwide imports Power BI dashboard

For this project I will be making a Power BI dashboard using the sample OLAP database [Worldwide Imports](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers), This sample has the structure of a Data Warehouse that consists of 8 dimension tables and 6 fact tables. I'll be using SQL as the data source for our dashboard and spreadsheets to generate a new table that contains a product category, by using AI to group each product into a category.

**[Dashboard file](https://drive.google.com/file/d/1YXyekD4utq5-67ltzhMarbSa7rumC_F5/view?usp=drive_link)

## Objectives
The objective of this project is to create a dashboard/report to obtain insights from the **Worldwide Imports** data warehouse using SQL to create KPI´s and Power BI to create Interactive reports and Power Query to clean data if needed. Create calculated measures for
KPI´ s or for charts.

### KPI´s
We need to analyze key indicators to gain quick insights about the business performance, for this we need to calculate the following metrics:

1. **Total revenue**
2. **Profit**
3. **Average order value**
4. **Total products sold**
5. **Average sales by salesperson**
6. **Average products per order**

### Charts
This project will have two pages, one dashboard with overall information, and a report with specific insights.
Main landing page:

1. **Stacked column chart**:
Create a column chart that displays the monthly revenue by product category to understand periods of higher sales.
2. **Donut chart**:
Create a donut chart that illustrates the total orders by category to help us identify patterns in order volumes.
3. **Table 1**:
Create a table that shows in a detailed way the information about orders, the table must   contain: Ordery Key, Order Date, Customer Key, Customer, City, State, Quantity, Total.
4. **Table 2**:
Create a second table with the information the employees that are incharge of sales, the table must have: Employees name, Average Revenue By Salesperson.
5. **Slicer**:
Create a Slicer button to select a specific year, this will help to navigate and obtain more precise information from the report.

### Products report:

1. **Stacked bar chart**:
Create a bar chart to display the total revenue by product category and product item, using the drill down mode will allow us to navigate through each category and gain more precise insights.
2. **Donut chart**:
Create a donut chart to illustrate the top 5 products sold distributed by the quantity, this allows us to identify the popularity of the products.
3. **Linechart**:
Create a line chart that shows the revenue and profit by a timeline, we can use drill down mode to change the date hierarchy and have deep insights about revenue and profit.
4. **Clustered column chart**:
Create a column chart that shows the amount of products purchased and the amount of products sold by year, this will help us know what products are being held in stock.
5. **Slicer**:
Create a slicer that allows us to select a specific period of time.

**ctrl + click to navigate using the buttons**
 
### KPI´s using SQL

Now I will use SQL to obtain the KPI´s
```sql 
-- 1. Total Revenue--
select SUM([Total Excluding Tax]) as Total Revenue
from Fact.Sale

-- 2. Profit--
select SUM(Profit)
from Fact.Sale

-- 3.  Average order value--
select AVG([Total Excluding Tax]) as AOV
from Fact.[Order]

-- 4. Total products sold--
Select SUM(Quantity)
from Fact.Sale

-- 5. Average sales by salesperson--
select distinct Employee, avg([Total Excluding Tax]) as gross_total_by_selesPerson
	from Fact.Sale A
		join Dimension.Employee B
		on A.[Salesperson Key] = B.[Employee Key]
		group by Employee
		order by gross_total_by_selesPerson desc

-- 6. Average products per order--
select AVG(Quantity)
from fact.[Order]
```
##### **Dashboard File**
[Power BI dashboard file](https://drive.google.com/file/d/1YXyekD4utq5-67ltzhMarbSa7rumC_F5/view?usp=drive_link)

##### **Sample Database**

[Microsoft SQL Samples](https://learn.microsoft.com/en-us/sql/samples/sql-samples-where-are?view=sql-server-ver16)