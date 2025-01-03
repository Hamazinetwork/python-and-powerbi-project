## Analyzing Data with Python and PowerBI

## Table of Content
  - [Problem Statement](#problem-statement)
  - [Tools Used](#tools-used)
  - [Data cleaning and Transformation](#data-cleaning-and-transformation)
  - [Data Analysis](#data-analysis)
  - [Conclusion](#conclusion)
  - [Recommendations](#recommendations)



### Problem Statement
A leading retail company aims to identify which products, locations, and categories to target or avoid amid growing demand and competition in the market.

### Tools Used
  - Python: Used for data cleaning and analysis.
```python
import pandas as pd
import matplotlib.pyplot as plt
```
  - Power BI: Utilized for visualization and report creation.
### Steps Taken
#### Data cleaning and Transformation
  1. Data Import and Setup:
     - Loaded the dataset and assigned it to a variable for easy reference.
       ```python
       path = r"C:\Users\mosho\Downloads\soft_drink_sales.xlsx"
       data = pd.read_excel(path)
       ```
     - Verified the imported columns:
       ```python
       data
       ```
  2. Setting Index:
     - Set the Order ID as the index for better data organization:
       ```python
       data = data.set_index('Order ID')
      ```
  3. Data Type Verification:
     - Checked the data types to ensure correctness:
       ```python
       data.dtypes
        ```
      - Converted Customer Zip Code to a string to avoid quantification:
        ```python
        data['Customer Zip Code'] = data['Customer Zip Code'].astype(str)
        ```  
  4. Null and Duplicate Check:
     - Checked for any null values (none found):
       ```python
       data.isnull().sum()
        ```
     - Verified there were no duplicates:
       ```python
       data.duplicated().sum()
        ```
#### Data Analysis
  1. State with Most Sales: Calculated total revenue by state:
     ```python
     StateRevenue = data.groupby('Customer State')['Revenue'].sum()
     StateRevenue.sort_values(ascending=False)
      ```
     <img width="956" alt="DS statehigestsale" src="https://github.com/user-attachments/assets/89aceff0-5700-4161-a716-6e6996cfabb0" />
     
  3. Monthly Sales Trend: Aggregated revenue by month:
     ```python
     RevenuePerDate = data.groupby('Purchase Date')['Revenue'].sum()
     RevenuePermonth = RevenuePerDate.resample('M').sum()
     plt.plot(RevenuePermonth)
     ```
     <img width="956" alt="DS monthlytrend" src="https://github.com/user-attachments/assets/8f83a7a4-398b-44df-a9db-b50d3e26588d" />
     
  5. Yearly Sales Trend: Aggregated revenue by year (similar to monthly calculation above).
     ```python
     RevenuePeryear = RevenuePerDate.resample('YE').sum()
     plt.plot(RevenuePeryear)
     ```
      <img width="953" alt="DS yeartrend" src="https://github.com/user-attachments/assets/6bbfc72c-bf98-4198-a057-076506de10bf" />
      
  7. Product Profitability:
     - Calculated revenue by product:
       ```python
       MostProfitableProduct = data.groupby('Product')['Revenue'].sum()
       MostProfitableProduct.sort_values(ascending=False)
       ```
       <img width="959" alt="DS revenuebyproduct" src="https://github.com/user-attachments/assets/8e7b6997-de5c-4a48-acc9-25c0ed80589f" />
       
     - Summed units sold by product category.
       ```python
       MostSoldCategory = data.groupby('Category')['Units Sold'].sum()
       MostSoldCategory.sort_values(ascending=False)
       ```
       <img width="959" alt="DS unitsoldpercategory" src="https://github.com/user-attachments/assets/858b66f3-a1ce-46b6-80bb-ab5030e190a1" />
       
  8. Category and Customer Analysis:
     - Calculated revenue and profit by product category.
       ```python
       CategoryofProductRevenuendProfit = data.groupby('Category')[['Revenue', 'Profit']].sum()
       ```
       <img width="959" alt="DS categoryprofitrevenue" src="https://github.com/user-attachments/assets/1bcbf8f0-aea6-4ac5-8977-acdc68aafe90" />
       
     - Identified top customers by revenue and units sold.
       ```python
       Customerwithhighestsalesndorder = data.groupby('Customer Name')[['Revenue', 'Units Sold']].sum()
       Customerwithhighestsalesndorder.sort_values(by=['Revenue', 'Units Sold'], ascending=False)
       ```
       <img width="959" alt="DS topcustomerunitsold" src="https://github.com/user-attachments/assets/7a1c499a-ae9e-4980-bc46-ec106e1c11c6" />


  #### Conclusion
  
  1. Sales Analysis
     - Top Performer: Minnesota had the highest overall sales.
     - Trend Over Years:
       - Sales peaked in 2020 at $15,473,581, with a slight decline in subsequent years.
       - 2023 saw a significant drop to $9,007,795.
     - Profit Comparison: Despite higher sales in 2020, 2022 had higher profitability.
  2. Product Analysis
     - Top-Selling Products: Herbal Tea led in both sales and profitability.
     - Price Range:
       - Products were mostly priced between $9 and $10.
       - Specific products like Lemonade, Green Tea, and Energy priced at $9, while others were $10.
  3. Customer and order Analysis
     - Most Ordered Category: Alcohol was the most frequently ordered, indicating strong market demand.
     - Product Performance: Herbal Tea and Green Tea performed well despite fewer options.
     - Order Frequency: Orders ranged from 1 to 2 per city, showing room for improvement in city-specific strategies.
    
       <img width="625" alt="Ds all1" src="https://github.com/user-attachments/assets/e53a1e24-6f96-4b89-b188-1aa16ea8c10c" />
    

     
       <img width="633" alt="Ds all2" src="https://github.com/user-attachments/assets/a710ff00-320a-418d-b07e-ba2707b9dca1" />
       
  #### Recommendations
  1. Sales Strategy
     - Address Decline: Develop strategies to counter the declining trend, focusing especially on the significant drop in 2023.
     - Profit Focus: Apply profitable strategies from 2022 more broadly.
  2. Product and Pricing
     - Promote Top Sellers: Increase marketing efforts for popular products like Black Tea.
     - Price Optimization: Review pricing of $10 products to ensure competitiveness.
  3. Category Management
     - Focus on Alcohol: Given the high demand, consider expanding or enhancing the product range in this category.
     - Improve Underperforming Categories: Apply insights from high-profit categories like Tea and Coffee to boost others.
  4. Order and Distribution
     - Enhance City Sales: Develop targeted marketing strategies for cities with low order frequencies.
     - Boost Order Quantity: Encourage customers to increase the quantity per order.


      








