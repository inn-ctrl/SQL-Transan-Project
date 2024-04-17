Question 1: Question 1: Which cities and countries have the highest level of transaction revenues on the site?

SQL Queries:
--FIND THE HIGHEST RANKING COUNTRY
 SELECT  country, SUM(CAST("totalTransactionRevenue" as integer)) As totals
 FROM all_sessions
 WHERE "totalTransactionRevenue" IS NOT NULL
 GROUP BY country
 ORDER BY totals DESC
 
--FIND THE HIGHEST RANKING CITY
SELECT  city, SUM(CAST("totalTransactionRevenue" as integer)) As totals
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY city
ORDER BY totals DESC

Answer: 

Country with highest level of transaction evenue: "United States"	13222160000
City with highest level of transaction revenue: "San Francisco"	1564320000

Question 2: Question 2: What is the average number of products ordered avg from visitors in each  country?--

SQL Queries:
SELECT  country, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
GROUP BY country
ORDER BY averageorders DESC

Answer:



Question 3: Question 3: Is there any pattern in the types (product categories) 
of products ordered from visitors in each city and country?

SQL Queries:

Answer:



Question 4: Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?

SQL Queries:

Answer:



Question 5: Question 5: Can we summarize the impact of revenue generated 

SQL Queries:

Answer:
