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
