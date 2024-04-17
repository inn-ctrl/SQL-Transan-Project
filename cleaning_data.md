What issues will you address by cleaning the data?

1. Before anything, I creaded the database and all the tables as needed. Next, I named all columns according to csv columns and then imported csv files.

Below are data cleaning issues I addressed: 

1. There are multiple headings across all tables due to pre-created pgadmin columns and csv columns. remove one.

   SQL CODES used
   
   DELETE FROM products
   WHERE name = 'name'
   
   DELETE FROM sales_report
   WHERE name = 'name'
   
   DELETE FROM sales_by_sku
   WHERE total_ordered = 'total_ordered'

   DELETE FROM all_sessions
   WHERE time= 'time'
   
3. The columns data type is 'text' throughout. Change to relevant data types

Queries:
Below, provide the SQL queries you used to clean your data.

ALTER TABLE all_sessions
ALTER COLUMN date
TYPE DATE
USING date::DATE

ALTER TABLE sales_by_sku
ALTER COLUMN total_ordered
TYPE INTEGER
USING total_ordered::integer

ALTER TABLE sales_report
ALTER COLUMN ratio
TYPE FLOAT
USING ratio::FLOAT

ALTER TABLE analytics
ALTER COLUMN bounces
TYPE INTEGER
USING bounces::integer

ALTER TABLE analytics
ALTER COLUMN unit_price
TYPE INTEGER
USING unit_price::integer


ALTER TABLE analytics
ALTER COLUMN timeonsite
TYPE INTEGER
USING timeonsite::integer

ALTER TABLE analytics
ALTER COLUMN pageviews
TYPE INTEGER
USING pageviews::integer

ALTER TABLE analytics
ALTER COLUMN units_sold
TYPE INTEGER
USING units_sold::integer

ALTER TABLE sales_report
ALTER COLUMN total_ordered INTEGER;

* The remaining columns, I changed data type inside SQL queries as needed to convert from text to numeric as follows:
- CAST("productQuantity" as integer
- CAST("productQuantity" as integer)
* selecting columns with capital letters was not possible. (only productquantity would work but not productQuantity). To work around that, I enclosed that name (productQuantity) in quotes ("productQuanityt") and casted it into numeric data type. 
