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
SELECT A,B,C
WHERE A> 15

```
