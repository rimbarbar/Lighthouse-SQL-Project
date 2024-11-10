Question 1: What are the top 5 most viewed products amongst all visitors?

SQL Queries:

SELECT 
    asess.product_SKU,
	asess.v2_product_name,
    COUNT(asess.full_Visitor_Id) AS view_count
FROM 
    all_sessions AS asess
GROUP BY 
    asess.product_SKU,
	asess.v2_product_name
ORDER BY 
    view_count DESC
LIMIT 5;


Answer: 
From my analysis, the product with the highest view count was "Google Men's 100% Cotton Short Sleeve Hero Tee White" with 284 views. Following this was "22 oz YouTube Bottle Infuser" with 245 views, then "YouTube Twill Cap" with 221 views, then "YouTube Custom Decals" at 211 views, then "YouTube Men's Short Sleeve Hero Tee Black" at 197 views. This data tells us that youtube merchandise seems to be very popular, which may be helpful information for the marketing department.


Question 2: Which city in the dataset has the most unique visitors?

SQL Queries:

SELECT 
    asess.city,
    COUNT(DISTINCT asess.full_Visitor_Id) AS unique_visitors
FROM 
    all_sessions AS asess
WHERE 
        asess.city != 'not available in demo dataset'
        AND asess.city != '(not set)'
GROUP BY 
    asess.city
ORDER BY 
    unique_visitors DESC
LIMIT 1;

Answer: Mountain view in the United States is the city with most unique visitors at 1,085.


Question 3: What percentage of viewers viewed at least one product?

SQL Queries:

WITH product_views AS (
    SELECT DISTINCT full_Visitor_Id
    FROM all_sessions
    WHERE product_SKU IS NOT NULL
)
SELECT 
    ROUND((COUNT(product_views.full_Visitor_Id) * 100.0) / 
          (SELECT COUNT(DISTINCT full_Visitor_Id) FROM all_sessions), 2) AS percent_viewed_product
FROM 
    product_views;

Answer: This query tells us how many visitors viewed at least one product. From my analysis, 100% of visitors viewed at least one product. By comparing this to the total unique visitors, we can better assess website engagement.  



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
