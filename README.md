# Kultra-Mega-Stores-Inventory-PROJECT
This is a complete Analysis documentation on the project Kultra-Mega-Stores-Inventory with Digital Skillup Africa (DSA).

This is my first project as a practical hands-on to validate the extent of the understanding of the classes I had with DSA. 
From the training, I found SQL classes most easier followed by Power-BI and this gives me the confidence to start with the SQL based-project first.

## Project Topic: Inventory Analysis

### Project Overview
This Inventory Analysis project aims to analyze the given data and present key insights and findings of the Inventory orders report from 2009 to 2012 of Kultra Mega Stores (KMS) which specialises in office supplies and furniture with its headquarters in Lagos.
By analysing the various parameters in the data given, I seek to understand the trends, identify areas for improvement and optimise inventory management to reduce cost and improve customer satisfaction and make reasonable recommendations based on the insight gotten to support the Abuja division of KMS.

### Data Sources
The primary source of Data used here is DSA Data Analysis Capstone Project Case Study 2: Kultra Mega Stores Inventory.csv.

### Tools Used
- Ms Excel for Data cleaning [Download Here](https://www.microsoft.com)
  - For Data Collection
  - For Data Cleaning
     1.   Data Manipulation
     2.   Data Munching
- SQL Server (For Querying and analysis)

### DATA CLEANING AND PREPARATION
 1. In the initial phase of the data cleaning and preparations, I perform the following actions;
 2. Data downloading and Inspection
 3. Handling missing varaiables
 4. Data cleaning and formating
 5. Data Importation into SQL Database Managent System.
    
### Exploratory Data Analysis (EDA)
EDA involved the exploring of the Data to answer some questions about the Data such as;
- Which product category had the highest sales?
- What are the Top 3 and Bottom 3 regions in terms of sales?
- What were the total sales of appliances in Ontario?
- KMS incurred the most shipping cost using which shipping method?
- Which consumer customer was the most profitable one?
- Which customer returned items, and what segment do they belong to?
- Which small business customer had the highest sales?
- Which Corporate Customer placed the most number of orders in 2009 – 2012?

### Data Analysis
This is where I included some basic lines of code or queries or even some of the DAX expresssions used during my analysis. I did the following DAX expressions for Discount, Profit, Unit-Price, Shipping-Cost and Product-Base-Margin to change their Datatypes.

``` SQL
Alter table KMS1
Alter Column Sales

alter table KMS1
alter column Sales decimal (10,2)

select * from KMS1

alter table KMS1
alter column Discount decimal (10,2)

alter table KMS1
alter column Profit decimal (10,2)

alter table KMS1
alter column Unit_Price decimal (10,2)

alter table KMS1
alter column Shipping_Cost decimal (10,2)

alter table KMS1
alter column Product_Base_Margin decimal (10,2)

**### DAX**
I then wrote the queries to answer some questions highlighted above after cleaning my Data.

select * from KMS1
WHERE Product_Base_Margin IS NULL

select * from KMS1

SELECT
      Order_Quantity,
      Sales,
      Discount,[dbo].[KMS1]
      Unit_Price,
      Profit,
      Shipping_Cost,
      Product_Base_Margin
      FROM KMS1
      where Product_Base_Margin IS NULL

     ALTER TABLE [dbo].[KMS1]
     ALTER COLUMN Product_Base_Margin decimal (10,2) NOT NULL
     



 SELECT * FROM KMS1

 ---1. Which product category had the highest sales? 

 select Product_Category,sum(Sales) AS HighestSales
 from KMS1
 group by Product_Category
 order by HighestSales desc

 ---    Ans: is Technology

---2. What are the Top 3 and Bottom 3 regions in terms of sales?

 select TOP 3
 Region, sum(Sales) AS TotalSales
 from KMS1
 group by Region
 order by TotalSales desc

 --- Ans: Top 3 Regions are West,Ontario and Prarie

 select TOP 3 
 Region, sum(Sales) AS TotalSales
 from KMS1
 group by Region
 order by TotalSales asc

 --- Bottom 3 Regions are Nunavut, Northwest Territories and Yukon

 ---3. What were the total sales of appliances in Ontario?

 select Region,sum(Sales) AS TotalSales
 from KMS1
 group by Region
 HAVING Region = 'Ontario'

            ---Ans: Total Sales of appliances in Ontario = 3063212.60 

 ---- 4. Advise the management of KMS on what to do to increase the revenue from the bottom 
 --- 10 customers

      select * from KMS1

      select Top 10
      Customer_Name, Product_Name, Product_Category, Order_Priority, Ship_Mode, Shipping_Cost, sum(Profit) AS TotalProfit
      from KMS1
      group by Customer_Name, Product_Name, Product_Category, Order_Priority, Ship_Mode, Shipping_Cost 
      order by TotalProfit asc

 --- The Management of KMS should do the following:
 --- i) Introduce customer service support to establish relationship with them
 --- ii) Offer targeted discount to them
 --- iii) Give rewards to encourage repeated transaction
 --- iv) Seek their opinion of how best to improve their services to them

  
 --- 5. KMS incurred the most shipping cost using which shipping method?

      select Ship_Mode,sum(Shipping_Cost) AS TotalShipping_Cost
      from KMS1
      GROUP BY Ship_Mode
      order by TotalShipping_Cost desc

   --- Ans: KMS incurred the most shipping cost by Delivery Truck

---- 6. Who are the most valuable customers, and what products or services do they typically 
----    purchase?
         select * from KMS1

         select Customer_Name, sum(profit) AS TotalProfit, sum(Sales) AS TotalSales
         from KMS1
         GROUP BY Customer_Name
         order by TotalProfit desc

         select count(DISTINCT Product_Name),sum(profit) AS TotalProfit, sum(Sales) AS TotalSales
         from KMS1
         GROUP BY Product_Name
         order by TotalProfit desc


--- 7. Which small business customer had the highest sales?

       select Customer_Name,sum(Sales) AS TotalSales
       from KMS1
       where Customer_Segment = 'Small Business'
       GROUP BY Customer_Name 
       order by TotalSales desc

--- 8. Which Corporate Customer placed the most number of orders in 2009 – 2012?

       alter table KMS1
       add Order_Year int
       select * from KMS1
       UPDATE KMS1
       SET Order_Year = year(Order_Date)

       select
          Customer_Name,Customer_Segment,count(DISTINCT Order_Year) AS Sumed_Year,
          sum(Order_Quantity) AS Most_Orders
          from KMS1
          WHERE Customer_Segment = 'Corporate'
          GROUP BY Customer_Name,Customer_Segment
          ORDER BY Most_Orders desc

--- 9. Which consumer customer was the most profitable one? 

         select TOP 1
         Customer_Name,Customer_Segment,sum(Profit) AS Most_Profitable
         from KMS1
         where Customer_Segment = 'Consumer'
         GROUP BY Customer_Name, Customer_Segment 
         order by Most_Profitable desc
 

---- 10. Which customer returned items, and what segment do they belong to?

         select *from KMS1
         select * from Order_Status

         select  KMS1.Order_ID,
         KMS1.Order_Date,
         KMS1.Customer_Name,
         KMS1.Customer_Segment,
         KMS1.Ship_Mode,
         Order_Status.Status
         FROM KMS1
         JOIN Order_Status
         ON Order_Status.Order_ID = KMS1.Order_ID
         WHERE Status = 'Returned'
 
---- 11. If the delivery truck is the most economical but the slowest shipping method and 
---  Express Air is the fastest but the most expensive one, do you think the company 
----  appropriately spent shipping costs based on the Order Priority? Explain your answer
         
         select * from KMS1
    --- Finding the relationship between ShipMode, OrderPriority and Shipping Cost
        
         select Ship_Mode, Order_Priority,Avg(Shipping_Cost) AS AvgShipping_Cost
         from KMS1
         GROUP BY Ship_Mode,Order_Priority

    --- We can then calaculate each average shipcost and order priority

         select Ship_Mode,Avg(Shipping_Cost) AS AvgShipping_Cost
         from KMS1
         GROUP BY Ship_Mode
         ORDER BY AvgShipping_Cost desc



                    select Ship_Mode,Order_Priority,Avg(Shipping_Cost) AS AvgShipping_Cost
            from KMS1
            GROUP BY Ship_Mode,Order_Priority
            ORDER BY Ship_Mode,Order_Priority 

 --- Bottom 3 Regions are Nunavut, Northwest Territories and Yukon


```
