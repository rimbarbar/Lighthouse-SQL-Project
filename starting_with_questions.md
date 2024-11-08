Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT 
    asess.city,
    asess.country,
    SUM(COALESCE(sales.total_ordered, 0) * anlyt.unit_price) AS estimated_revenue
FROM 
    all_sessions asess
JOIN 
    analytics anlyt ON asess.visit_Id = anlyt.visit_Id
LEFT JOIN 
    sales_by_sku sales ON asess.product_SKU = sales.product_SKU
WHERE 
    anlyt.unit_price IS NOT NULL
GROUP BY 
    asess.city, asess.country
ORDER BY 
    estimated_revenue DESC;


Answer:

From my analysis I found that the highest estimated revenue by city and country shows the highest revenue from a category labeled as "Not available in demo dataset," with a total of $13,469,795. This likely indicates missing or incomplete geographic data for some sessions. Following this, Mountain View, California, in the United States, ranks second with an estimated revenue of $6,729,805. Sunnyvale, California, comes next with an estimated revenue of $2,781,405, while New York, New York, follows with $1,920,178 in estimated revenue. Lastly, San Francisco, California, completes the top five cities with an estimated revenue of $1,755,518. 


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT 
    asess.city,
    asess.country,
    AVG(COALESCE(sales.total_ordered, 0)) AS avg_products_ordered
FROM 
    all_sessions asess
JOIN 
    analytics anlyt ON asess.visit_id = anlyt.visit_id
LEFT JOIN 
    sales_by_sku sales ON asess.product_SKU = sales.product_SKU
GROUP BY 
    asess.city, asess.country
ORDER BY 
    avg_products_ordered DESC;


Answer:

Based on my query, the average number of products ordered by visitors in each city and country varies significantly. Shinjuku, Japan, has the highest average at approximately 199 products ordered per visitor. Following closely are Sacramento and Rio de Janeiro, both with an average of 189 products ordered. A category labeled as "Not available in demo dataset" for Croatia shows an average of 135 products ordered. Finally, Rexburg, United States, has an average of 114 products ordered. These results indicate varying levels of product orders across different cities, with some cities showing much higher average numbers than others.




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries: 

SELECT 
    asess.city,
    asess.country,
    STRING_AGG(DISTINCT asess.V2_Product_Category, ', ') AS product_categories
FROM 
    all_sessions asess
JOIN 
    analytics anlyt ON asess.visit_Id = anlyt.visit_Id
WHERE 
    asess.city != 'not available in demo dataset'
    AND asess.city != '(not set)'
GROUP BY 
    asess.city, asess.country
ORDER BY 
    asess.city, asess.country;

Answer:

From my data analysis, there do seem to be certain patterns emerging. In major cities across the United States, India, and Europe, categories like "Men's T-Shirts," "Accessories," and "Bags" are significantly popular, indicating a consistent interest in apparel and lifestyle items. Additionally, “Shop by Brand/YouTube” appears frequently in various international cities, suggesting a widespread appeal of brand-specific shopping. Cities in technologically advanced countries like Japan and Germany show interest in "Electronics" and "Audio" categories, which reflects a demand for tech-related products. Meanwhile, cities in countries like Argentina and Turkey show a more selective engagement with categories, often focusing on bags and apparel basics, highlighting the regional product preferences.


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







