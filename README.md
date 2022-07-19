# AtliQ Hardware Sales Insights

### AtliQ Hardware
Is a company which supplies computer hardware and peripherals to many clients across India.\
The company has a head office in Delhi and regional offices throughout India.

---

### Business Issue
The sales director is facing a lot of challenges. The marketing is growing dynamically and then he’s struggling in terms of tracking the sales, needing more accurate insights about the company sales, and then take the necessary decisions.

---

### Solution
- Create a simple and informative dashboard about the company sales.
- I used **`SQL`** queries in **`MySQL Workbench`** to take a look into the data and **`Tableau`** for **`ETL`** and **`Visualizations`** to create the insights dashboard.

---

### Data Overview

#### `# Tables`
    
<table>
<tr><th>1. transactions</th><th>2. customers</th><th>3. date</th><th> 4. products </th><th> 5. markets </th></tr>
<tr><td>

|Field Name|Description|
|----|---|
|Product Code||
|Customer Code||
|Market Code||
|Order Date||
|Sales Qty||
|Sales Amount||
|Currency||
|Profit Margin||
|Profit||
|Cost||

</td><td>

|Field Name|Description|
|---|---|
|Customer Code||
|Custmer Name||
|Customer Type||

</td><td>

|Field Name|Description|
|---|---|
|Date||
|Cy Date||
|Year||
|Month Name||
|Date Yy Mmm||
	
</td><td>
	
|Field Name|Description|
|---|---|
|Product Code||
|Product Type||

</td><td>

|Field Name|Description|
|---|---|
|Markets Code||
|Markets Name||
|Zone||


</td></tr> </table>

#  
#### `# Data Analysis Using SQL`

1. Show all customer records

    `SELECT * FROM customers;`

1. Show total number of customers

    `SELECT count(*) FROM customers;`

1. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

1. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
1. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

1. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`
# 
#### `# Insights`
After a quick data exploration in MySQL, here are some initial findings:
- The database contains 5 tables: customers, date, markets, products, and transactions.
- There are 17 markets, 279 products, and 38 customers.
- The observation period is from OCT 2017 to JUN 2020.
- The total revenue in 2020 was ₹ 142.22 M, 57.7% less than 2019, which was ₹ 336.02 M.
- Most of the transactions data are in INR(₹) currency, but we have 2 records in US($) currency. 
- And we got some garbage values in sales amount and market column. We’re going to deal with it in the ETL process.

---

### ETL(Extract, Transform, Load)
Once I know the basic features of the data I have to work with, I imported the MySQL database into Tableau to do the necessary transformations and end up with a simple, reliable, and useful dashboard.

---

### Data Modeling Step
We got five tables and we need to ensure that the tables are correctly connected.
- Main Table: transactions

|Table|Column|Main Table Column|
|---|---|---|
|customers|Customer_Code|Customer_Code|
|date|date|Order_Date|
|products|Market_Code|Market_Code|
|markets|Product_Code|Product_Code|

---

### Filtering, Cleaning and Adding New Columns
- As the company is operating only in India, filtered out “Paris” and “New York” in the sales markets table.
- The “currency” column (in transactions table) have 2 USD currency values, So created a new column called “Sales”, where all the sales_amount is in INR Currency.

---

### Dashboards
The two dashboards shows all the main information about the company sales.
- Dashboard 1: Sales Insights
<div class='tableauPlaceholder' id='viz1658228506034' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;At&#47;AtliqHardware&#47;AtliqHardware&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='AtliqHardware&#47;AtliqHardware' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;At&#47;AtliqHardware&#47;AtliqHardware&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-GB' /></object></div>

    - Revenue
    - Net Profit
    - Revenue by Market
    - Profit Trend by Market
    - Revenue by Top 10 Products
    - Profit Trend by Top 10 Products

- Dashboard 2: Loss Analaysis
<div class='tableauPlaceholder' id='viz1658228711044' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;At&#47;AtliqHardware&#47;LossAnalysis&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='AtliqHardware&#47;LossAnalysis' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;At&#47;AtliqHardware&#47;LossAnalysis&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-GB' /></object></div>

    - Loss Amount
    - Markets Which creating Loss
    - Top 10 Lossing Products

It can be filtered by YEAR and it's a interactive Dashboard i.e, each other insights are inter-related and can be seen in any respects. So the sales director can have a deeper and quick view of the sales to support his decision making process.

---
### Final Report
Based on the dashbaords insights, I have made some conclusions and recommendation that Sales Marketing team should/can consider making a sales strategy.

#### # Conclusions
- Sales were rapidly decreasing in 2020 compared to 2019 by around 57.7%.
- Highest revenue generated from Markets such as Delhi NCR, Mumbai, Ahmedabad, Bhopal, Nagpur, and so on.
- Highest quantities sold in the Market such as Delhi NCR, Mumbai, Nagpur, Kochi, Ahmedabad, and so on.
- Majority of the sales were takes place in the month of January followed by November and March.

#### # Recommendation
- Make a new sales strategy for lucknow since its showing lowest revenue and negative profit margin and if possible so as for Surat and Bhubhaneshwar also.
- try to increase sales quantity in Patna, Surat and Kanpur since they have lowest sales quantity.
- start target campagin for Prod047 and Prod061 since they two are the most profitable and most selling products.
- try to give special benefits to Electronics and Excel stores as they are most profitable customers.
- make campgain strategy for mid year as they are showing high sales among other months.

---

### References
- *Project Inspiration: [codebasics](https://youtube.com/playlist?list=PLeo1K3hjS3usDI9XeUgjNZs6VnE0meBrL) YouTube channel.*
- *Project Data: [Google Sheet](https://docs.google.com/spreadsheets/d/1cidC_V9YrS789-ZYTdAM1OgIXZVa_XfkRVy5Cyp3Qk8/edit?usp=sharing) | [SQL Dump File]()*
