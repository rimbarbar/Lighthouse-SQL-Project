What issues will you address by cleaning the data?

Queries:
Below, provide the SQL queries you used to clean your data.


The first thing I noticed before even creating the tables was the lack of consistency in the column title formatting (orderedQuantity vs. unit_price). To fix this issue, I used the following query and repeated for the remaining tables and columns:

-- Renaming columns to snake_case for sales_report
ALTER TABLE sales_report 
    RENAME COLUMN stocklevel TO stock_level;

ALTER TABLE sales_report 
    RENAME COLUMN restockingLeadTime TO restocking_lead_time;

Then after diving into the data, I noticed all the columns with null values, the columns that were completely empty (all_sessions type, analytics userid), and the columns that were redundant or unnessacary.

I used the following query to get the count of Null values in each column in a table and repeated the query for all tables:

SELECT 
    SUM(CASE WHEN full_visitor_id IS NULL THEN 1 ELSE 0 END) AS full_visitor_id_null_count,
    SUM(CASE WHEN channel_grouping IS NULL THEN 1 ELSE 0 END) AS channel_grouping_null_count, 
. . . 
FROM all_sessions;

From the results, I went over which columns were unnecessary and weren’t contributing meaningful data and decided to drop those columns from the dataset using the following query:

The columns I dropped were:

All 3 eccomerce_action columns from the all_sessions table.

Also, there were values in the sales_report table and the sales_by_sku table that didn’t match up, so I used the query below to match them up.

INSERT INTO sales_report (productSKU, total_ordered, name, stockLevel, restockingLeadTime, sentimentScore, sentimentMagnitude, ratio)
VALUES 
('GGOEGAAX0568', 3, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEAHPB076114', 1, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEGEVB070599', 0, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEGAAJ059113', 1, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEGEHQ072599', 0, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEGAAX0732', 0, NULL, NULL, NULL, NULL, NULL, NULL),
('GGOEGAXJ065555', 3, NULL, NULL, NULL, NULL, NULL, NULL)
ON CONFLICT (productSKU) DO NOTHING;

