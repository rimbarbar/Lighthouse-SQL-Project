What are your risk areas? Identify and describe them.

  In my analysis, I found several potential risk areas that could impact the accuracy and reliability of my data results:

1. There is a high occurence of duplicate entries, especially in critical columns such as full_Visitor_Id and visit_Id in the all_sessions table. Duplicates in these columns (which should be primary key columns) could lead to inaccurate counts for visitors or transactions.
2. There are multiple columns in the dataset with null or empty values, like item_Quantity, total_Transaction_Revenue, and product_SKU. These columns are essential for calculations and analysis. These null values severly impact revenue and unique product view calculations, potentially skewing results and causing query errors.

QA Process: Describe your QA process and include the SQL queries used to execute it.

  To address these risk areas, I designed a QA process to validate the data. Here are my steps below:

1. I checked for duplicate full_Visitor_Id and visit_Id combinations in the all_sessions table and for duplicates in product_SKU in the sales_report table. My data output for the all_sessions table resulted in 549 rows all with occurence counts of 2. For the sales_report table, I got no data output, signifying no duplicates in the product_sku column.

Queries:
-- Check for duplicate visitor-session pairs in all_sessions
SELECT full_Visitor_Id, visit_Id, COUNT(*) AS occurrence_count
FROM all_sessions
GROUP BY full_Visitor_Id, visit_Id
HAVING COUNT(*) > 1;

-- Check for duplicate product_SKU records in sales_report
SELECT product_SKU, COUNT(*) AS occurrence_count
FROM sales_report
GROUP BY product_SKU
HAVING COUNT(*) > 1;


2. Next I wanted to validate the unique counts for visitors and products viewed to ensure data accuracy.

- To check the total unique visitors I used the query below and got 14,223 unique visitors.

SELECT COUNT(DISTINCT full_Visitor_Id) AS total_unique_visitors
FROM all_sessions;

- To check the amount of unique visitors by referring sites, I used the query below and found that the most unique visitors came by organic search with 8,207 and direct referral at 2,805, while the least was from (other) with 5 unique visitors. 

SELECT channel_Grouping, COUNT(DISTINCT full_Visitor_Id) AS unique_visitors
FROM all_sessions
GROUP BY channel_Grouping;

- To check the amount of unique products viewed by each visitor, I used the query below and got 14,223 rows, all having a unique products viewed count of 1.

SELECT full_Visitor_Id, COUNT(DISTINCT product_SKU) AS unique_products_viewed
FROM all_sessions
WHERE product_SKU IS NOT NULL
GROUP BY full_Visitor_Id;

3. Next I wanted to check for null values in the columns that were crucial to my analysis. I found 15,134 nulls in item_quantity, 15,053 nulls in revenue, and 0 nulls in product_sku. I used the following query:

SELECT 
    COUNT(*) FILTER (WHERE item_quantity IS NULL) AS null_item_quantity,
    COUNT(*) FILTER (WHERE total_Transaction_Revenue IS NULL) AS null_revenue,
    COUNT(*) FILTER (WHERE product_SKU IS NULL) AS null_product_sku
FROM all_sessions;


4. Lastly, I wanted to check for outliers in the transaction revenue column so I calculated the average and standard deviation of total_Transaction_Revenue and identified any values that were significantly above or below average. For my first query I got an avg revenue of 176312469 and a standard deviation of 221871086. For my second query, I got 3 cities in the United States (all cities were "not available in demo dataset") with values of 849700000, 1015480000, and 1005500000. Although I didn't use the transaction revenue column since the majority of it contained null values, this information would be critical to know for my analysis if I were to populate that column with data one day. 

-- Calculating average revenue and standard deviation
SELECT AVG(total_Transaction_Revenue) AS avg_revenue, 
       STDDEV(total_Transaction_Revenue) AS stddev_revenue
FROM all_sessions
WHERE total_Transaction_Revenue IS NOT NULL;
-- Selecting rows with revenue significantly above or below average				 
SELECT city, country, total_Transaction_Revenue
FROM all_sessions
WHERE total_Transaction_Revenue > (SELECT AVG(total_Transaction_Revenue) + 3 * STDDEV(total_Transaction_Revenue) 
                                 FROM all_sessions);

