Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
Finding countries that have the highest level of transaction revenues

SELECT  country, SUM(CAST("totalTransactionRevenue" as integer)) As totals
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL
GROUP BY country
ORDER BY totals DESC

Finding cities that have the highest level of transaction revenues

SELECT  city, SUM(CAST("totalTransactionRevenue" as integer)) As totals
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY city
ORDER BY totals DESC


Answer:


Country with highest level of transaction evenue: "United States"	13222160000
City with highest level of transaction revenue: "San Francisco"	1564320000

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries: 

a. average of products ordered in each country

SELECT  country, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
GROUP BY country
ORDER BY averageorders DESC

b. average of products ordered in each city

SELECT  city, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL 
AND city != 'not available in demo dataset' 
AND city != '(no set)'
GROUP BY city
ORDER BY averageorders DESC

Answer: 

Country average

|country      |averageorders         |
|-------------|----------------------|
|Spain        |10.0000000000000000   |
|United States|4.0238095238095238    |
|Colombia     |1.00000000000000000000|
|Finland      |1.00000000000000000000|
|France       |1.00000000000000000000|
|Argentina    |1.00000000000000000000|
|Ireland      |1.00000000000000000000|
|Mexico       |1.00000000000000000000|
|India        |1.00000000000000000000|
|Canada       |1.00000000000000000000|



city average: 
|city         |averageorders         |
|-------------|----------------------|
|Madrid       |10.0000000000000000   |
|Salem        |8.0000000000000000    |
|Atlanta      |4.0000000000000000    |
|Houston      |2.0000000000000000    |
|New York     |1.1666666666666667    |
|Dallas       |1.00000000000000000000|
|Detroit      |1.00000000000000000000|
|Dublin       |1.00000000000000000000|
|Los Angeles  |1.00000000000000000000|
|Mountain View|1.00000000000000000000|
|Palo Alto    |1.00000000000000000000|
|San Francisco|1.00000000000000000000|
|San Jose     |1.00000000000000000000|
|Seattle      |1.00000000000000000000|
|Sunnyvale    |1.00000000000000000000|
|Ann Arbor    |1.00000000000000000000|
|Bengaluru    |1.00000000000000000000|
|Chicago      |1.00000000000000000000|
|Columbus     |1.00000000000000000000|


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







