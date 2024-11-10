# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
For this project, I wanted to transform and analyze e-commerce data using SQL to answer key questions related to customer behavior, product performance, and revenue insights. My goal was to demonstrate my skills in data cleaning, query writing, and analysis, and to extract meaningful insights that could drive business decisions. I focused on uncovering patterns in visitor interactions, revenue generation, and product popularity across different regions.

## Process
### Step 1: Data Preparation and Exploration
I started by reviewing each table's structure and checking for any data quality issues, such as duplicate records or null values in key columns like productSKU, itemQuantity, and totalTransactionRevenue. This initial step helped me understand the dataset’s potential issues and determine how to approach the cleaning process.
###Step 2: Cleaning and Transforming the Data
To ensure accurate results, I addressed duplicate records and handled missing values. I used SQL queries to check for null values in essential columns and implemented data transformations as needed, like casting data types and creating additional views to manage cleaned data. For example, I created views to handle null values in the itemQuantity column by calculating product views per visitor as a way to gauge interest and engagement.
###Step 3: Data Analysis and Querying
With clean data, I focused on writing queries to answer specific questions, such as finding total unique visitors, unique products viewed by each visitor, and calculating the percentage of visitors who made purchases. I also calculated total revenue by city and analyzed which products were the most popular in each region.

## Results
Through this analysis, I discovered several insights:
- I identified the top-selling products in various cities and regions, highlighting specific product preferences that could inform targeted marketing efforts.
- I calculated the percentage of visitors who viewed products and subsequently made purchases, providing insights into customer engagement and conversion.
- I identified key revenue-generating cities, which could guide future regional marketing strategies.
These findings helped me understand customer behavior and regional trends that could be valuable for business growth.

## Challenges 
One of the main challenges I had was handling null values in critical columns like item_Quantity, which impacted revenue calculations. I addressed this by using other measures, such as views of unique products by each visitor. Additionally, managing joins between tables without direct keys required creative use of subqueries and views to link data effectively. Inconsistent column names across tables (like productSKU vs. SKU) also complicated the joins, requiring additional transformations to standardize these fields. Finally, the visit_start_time column required transformation to a readable format, and duplicate records occasionally interfered with analysis, so I implemented further cleaning steps as needed.

## Future Goals
With more time, I would have performed additional data cleaning, particularly focusing on standardizing column names across tables to ensure consistency (productSKU vs. SKU). I would also like to further clean up duplicates to maintain data integrity. Additionally, I would delve deeper into customer journey analysis to identify repeat customers and calculate customer lifetime value. Exploring the sentiment_Score column for potential impacts on purchasing behavior could provide valuable insights into how product perception affects sales. Finally, implementing data visualization tools would help present these insights more clearly to stakeholders.
