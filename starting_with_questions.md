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
Products ordered in each country:

SELECT country, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
ORDER BY "productQuantity"

Products ordered in each city:

SELECT city, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
AND city != 'not available in demo dataset'
AND city != '(not set)' 
ORDER BY "productQuantity"

Answer:

Observation analysis of product categories in countries:

*spain is an outlier and USA are outliers compared to other countries
*buyers bought specific products in larger quantities in these countries

Observatin analysis of product categories in cities:

* Madrid and USA cities are outliers outlier
* Specific products were bought in larger quantities in these cities compared to others (Madrid, Atlanta, Salem)


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries: (To get top-selling product from each country/city, we use a window function that ranks all countries/cities based on the product quantities, then use a subquery to filter only those countries with the first rank.

--a. top-selling product from each country
/*Main query*/
SELECT * 
FROM (
--1. rank every product based on countries and order them by product names in a subquery
	SELECT al.*,
	RANK() OVER(partition by country ORDER BY"v2ProductName"  ) as product_rank
	FROM all_sessions al
-- 2. filter missing values 
	WHERE country != 'not available in demo dataset'
	AND country != '(not set)'
	AND "productQuantity" IS NOT NULL
) AS ranked_country
-- 2. extract only the first from each country by using a subquery
WHERE ranked_country.product_rank = 1


-- b. top-selling product from each city
/*Main query*/
SELECT * 
FROM (
--1. rank every product based on city and order them by product names in a subquery
	SELECT al.*,
	RANK() OVER(partition by city ORDER BY"v2ProductName"  ) as product_rank
	FROM all_sessions al
-- 2. filter missing values 
	WHERE city != 'not available in demo dataset'
	AND city != '(not set)'
	AND "productQuantity" IS NOT NULL
) AS ranked_city
-- 2. extract only the first from each city by using a subquery
WHERE ranked_city.product_rank = 1


Answer:

Is there any pattern? Spain and United States are visible outliers. 

-- Spain is an outlier with the product quantity considerably higher than other cities. United states also consumed more quanitities than other countries. 


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

-- we use GROUP BY to totalize revenues generated from each country--
SELECT country, SUM("totalTransactionRevenue"::int) as transcountry
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL
AND country != '(not set)'
GROUP BY country

-- we use GROUP BY to totalize revenues generated from each city--
SELECT city, SUM("totalTransactionRevenue"::int) as transcountry
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL
AND city != 'not available in demo dataset'
AND city != '(not set)'
GROUP BY city


Answer:
Summary of countries and total revenues: 

Country		transcountry
"Australia"	358000000
"Canada"	82160000
"Israel"	602000000
"Switzerland"	16990000
"United States"	13222160000


Summary of cities and total revenues: 

city		transcity
"Atlanta"	854440000
"Austin"	157780000
"Chicago"	449520000
"Columbus"	21990000
"Houston"	38980000
"Los Angeles"	479480000
"Mountain View"	483360000
"Nashville"	157000000
"New York"	598350000
"Palo Alto"	608000000
"San Bruno"	103770000
"San Francisco"	1564320000
"San Jose"	262380000
"Seattle"	358000000
"Sunnyvale"	992230000
"Sydney"	358000000
"Tel Aviv-Yafo"	602000000
"Toronto"	82160000
"Zurich"	16990000





