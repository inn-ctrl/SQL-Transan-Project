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

Question 2: Question 2: What is the average number of products ordered avg from visitors in each city and country?

SQL query: 

--avg from visitors in each  country?--
SELECT  country, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
GROUP BY country
ORDER BY averageorders DESC
--1. avg from each visitors in each city 

SELECT  city, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL 
AND city != 'not available in demo dataset' 
AND city != '(no set)'
GROUP BY city
ORDER BY averageorders DESC

Answer:

country average 

"Spain"	10.0000000000000000
"United States"	4.0238095238095238
"Colombia"	1.00000000000000000000
"Finland"	1.00000000000000000000
"France"	1.00000000000000000000
"Argentina"	1.00000000000000000000
"Ireland"	1.00000000000000000000
"Mexico"	1.00000000000000000000
"India"	1.00000000000000000000
"Canada"	1.00000000000000000000

city average: 

"Madrid"	10.0000000000000000
"Salem"	8.0000000000000000
"Atlanta"	4.0000000000000000
"Houston"	2.0000000000000000
"New York"	1.1666666666666667
"Dallas"	1.00000000000000000000
"Detroit"	1.00000000000000000000
"Dublin"	1.00000000000000000000
"Los Angeles"	1.00000000000000000000
"Mountain View"	1.00000000000000000000
"Palo Alto"	1.00000000000000000000
"San Francisco"	1.00000000000000000000
"San Jose"	1.00000000000000000000
"Seattle"	1.00000000000000000000
"Sunnyvale"	1.00000000000000000000
"Ann Arbor"	1.00000000000000000000
"Bengaluru"	1.00000000000000000000
"Chicago"	1.00000000000000000000
"Columbus"	1.00000000000000000000


Question 3: Question 3: Is there any pattern in the types (product categories) 
of products ordered from visitors in each city and country?

SQL Queries:
SELECT country, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
ORDER BY "productQuantity"

-- analysis of product categories in countries
-- analysis of product categories in cities

SELECT city, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
AND city != 'not available in demo dataset'
AND city != '(not set)' 
ORDER BY "productQuantity"




Answer:
observations about countries: 
	 --* spain is an outlier and USA are outliers compared to other countries
	 --* buyers bought specific products in larger quantities in these countries
  
bservations about the cities: 
	 --* Madrid and USA cities are outliers outlier
	 --* Specific products were bought in larger quantities in these cities 
	 -- compared to others (Madrid, Atlanta, Salem)

Question 4: Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?

SQL Queries:

Answer:



Question 5: Question 5: Can we summarize the impact of revenue generated 

SQL Queries:

Answer:
