# Lita Sales Analysis 

### Table of content 

- [project Overview](#project-overview)
- [Data description](#data-description)
- [Data Sources](#data-sources)
- [Tools Used](#tools-used)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Insights](#insights)
- [Recommendation](#recommendation)

### Project Overview 
---

This project focuses on analyzing the sales performance of a retail store. By exploring the sales data, it aim to uncover key insights, including identifying top-selling products, evaluating regional performance, and analyzing monthly sales trends. The findings will provide valuable information for strategic decision-making and optimizing sales strategies.

### Data description
---

-OrderID: A distinct identifier assigned to each order.

-CustomerId: A distinct identifier for customers.

-Product: Items being sold.

-Region: The geographical location of each customer. 

-OrderDate: The date each order was made.

-Quantity: The number of items purchased.

-UnitPrice: The cost price of each product.
-Total Sales: The total sales generated from each product. 

-Revenue: The total revenue generated from each product sold.  


### Data sources 
---

Sales data:The primary dataset used  for this analysis is "LITA Salesdata.Csv" file, containing detailed information about each sale made by the company. 

### Tools used 
---

- Excel - Data cleaning and Analysis [*Download here*](https://www.microsoft.com/en-ng/)
- Sql Server - Data Analysis [Download here] (
- Powerbi - Visualization and building dashboard Reports -
   [*Download here*] (https://powerbi.microsoft.com/desktop/)


  ### Data cleaning and Preparation
---
  In the initial data preparation phase, we performed the following task:
  1. Data loading/Inspection
  2. Delete duplicate data
  3. checked for missing values
  4. check for null values 

  ### Exploratory Data Analysis
---
  EDA invloved exploring the sales data to answer key questions, such as:

  
  -  Total sales for each product
  - The highest selling product 
  - what is the number of sales transaction in each region
  - Find the top 5 customers by total purchase amount
  - Product with no sales in the last quarter
  - The percentage of total sales conributed by each region
  - The monthly sales total for the current year.

 ### Data Analysis
 ---
 - Total sales: To get a well detailed insight to the over all sales, we had to get a column for the revenue by multiplying the quantity by unitprice. which will give us an oversight of how much was generated by the company in the given time. Formula used: ```=product(number1,[number2])```
- Top performing product: products were analyzed to know our best selling products, regions that pulled the best sales, Months that had the most revenue. This analyzes was done with pivot table by summarising our data.
- Metrics: we calculated metrics such as average sales per each product.

  ![Screenshot 2024-11-06 104238](https://github.com/user-attachments/assets/1e0b9ac9-9958-45be-bf6d-b0329bfe4145)
  
![Screenshot 2024-11-06 130957](https://github.com/user-attachments/assets/7a4f8207-a079-4b53-b4e1-beca6dfa51aa)

 ### SQL Analysis

  
### 1.Total sales for each product category---
```
select product, sum (total_sales)as totalsale
from [dbo].[VW_Sales_Data]
group by product
```
select distinct product, sum (total_sales)as totalsale
from [dbo].[VW_Sales_Data]
group by product

### 2.number of sales transactions in each region----
```
select  region, count(Quantity) as numberofsales
from [dbo].[VW_Sales_Data]
group by region
```
### 3.Highest selling product by total sales value---
```
select top 1 product, sum (total_sales)as totalsale
from [dbo].[VW_Sales_Data]
group by product
order by 2 desc
```

### 4. Total revenue by product
```
select product, sum(quantity*unitprice) as revenue
from [dbo].[VW_Sales_Data]
group by product;
```

### 5.Monthly sales total by current year
```
select OrderDate, sum(Total_sales) Total_MonthlySales
from [dbo].[VW_Sales_Data]
where OrderDate > '2023-12-31'
group by OrderDate
order by 2 desc
```
```
select OrderDate, sum(Total_sales) Total_MonthlySales
from [dbo].[VW_Sales_Data]
where OrderDate like '2024%'
group by OrderDate
order by 2 desc
```

### 6.Top 5 customers by Total purchase Amount
```
select   TOP 5 sum(Total_sales) as Highest_sales , customer_id
from [dbo].[VW_Sales_Data]
group by customer_id
ORDER BY 1 desc
```

### 7.percentage of total sales contributed by each region
```
select region, sum(Total_sales) as Sales_Total,
(sum(Total_sales)*100/(select sum(Total_sales) from [dbo].[VW_Sales_Data])) as Sales_percentage
from [dbo].[VW_Sales_Data]
group by region
order by Sales_Total
```

### 8.Identify products with no sales in the last quarter----
```
select product,Total_sales
from [dbo].[VW_Sales_Data]
where Total_sales = 0  and OrderDate between '2024-05-31' and '2024-08-31'
```

### Powerbi Dashboard visualization

we were able to visualize some of our analyzes with powerbi dashboard for deeper insights. 

 ![Screenshot 2024-11-07 162135](https://github.com/user-attachments/assets/129c9168-5bc6-4150-94dd-a1d554233822)



 ### Insights
 ---
After critical analyzes of the sales trend and overall performance, we were able to draw conclusions and understand the data. The following are insights gotten from the analyzes.
- The count of total quantity of product sold is "68,461"
 -The total revenue made from all products is "$2,101,090.00" which is decent amount for the comapny of that capacity and the average revenue being " 211.78". 
 _ The product with the highest revenue is shoes, followed closely by shirt and hat, while gloves, Jackets and socks are the lowest. This gives us an understanding that our customers priotize items that are fashionable over items that prevent colds and harmattan. The weather would make customers not to really buy jackets, shoes and socks as they prevent cold and they country is more sunny than chilly.The items are bought in just few times there is cold, which is the reason for the low sales from them.
 - Among the four regions"South, East, North and West", South gave us the most revenue making up "44%" of the total revenue, East gave us "23%", North gave us "18%" while West gave us "14%" of the revenue. This analysis shows the huge gap in revenue made by the south region as compared to other regions.
 - South sold the most quantity of products. 
 - we foujd out that there are no period where we recorded zero sales. Products were sold every month, no matter how little.
 - The analysis and visualization showed that the month of february had the highest sales,the first two quarter of the year gave us almost the same revenue while the last quarter gave us the lowest revenue.The sales gave a huge shoot up in february, making a big difference compare to other months in the first two quarters.

   ### Recommendation
   ---
   - They should invest more in advertisement and branding to bring in more sales. Though the revenue made is on the safe side and shows the comapny is growing but they can always generate more. 

   - The company should reduce the quantity being produced for "Gloves, Jacket and Socks" since the demand for it is quite low and they should always have in stocks the products that are in higher demand "Shoes, Shirts, Gloves".
   -  There should be more investment in regions other than South, reasons for the growth in the south should be studied and implemented in other regions. some factors that maybe affecting the low performance in the regions, which maybe looked into are; Location of the company, branding in those regions, staff perfomance, Advertisement and awareness of the brands in those regions.
   -  Products should be produced more in the first two quarter of the year especially in february and less produced in the last quarter as the demand is low. 

 
