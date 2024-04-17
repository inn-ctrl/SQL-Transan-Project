# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
This is the project about product sales in the ecommerce business. The end objective is to use SQL query to come up with insights that respond to business prompts. 

Goals: 
- Populating data in the database and cleaning them for proper analysis
- Applying SQL queries learned so far to solve prompted questions
- Observing created queries to come up with business insights

## Process
### Setting up Database and Data Cleaning
* Setting up Database
  The database was set up in Postgresql using provided datasets. The following tables was created as a result:
  - products table
  - sales_by_sku table
  - sales_report table
  - analytics table and
  - all_sessions table
 
* Data cleaning
  - during importation, there were underlying table columns that made it difficult to extract the information. That was deleted using the queries provided in 'cleaning_data' section page.
  - similarly, all columns were given the 'text' data type for the ease of importation. They were converted to relevant data types as the project advanced
  - 
### Data Analysis 
Here are teh queries that were used to analyse the data: 
- Ranking the countries according to the highest level of transaction revenues. This was achieved by the following SQL query:
  
 SELECT  country, SUM(CAST("totalTransactionRevenue" as integer)) As totals
 FROM all_sessions
 WHERE "totalTransactionRevenue" IS NOT NULL
 GROUP BY country
 ORDER BY totals DESC

- Ranking the cities according to the highest level of transaction revenues. This was achieved by the following SQL query:
  
SELECT  city, SUM(CAST("totalTransactionRevenue" as integer)) As totals
FROM all_sessions
WHERE "totalTransactionRevenue" IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY city
ORDER BY totals DESC

- Finding average number of products that was ordered from each country. This was achieved by the following SQL query:
SELECT  country, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
GROUP BY country
ORDER BY averageorders DESC
- Finding the average number of products that was ordered from each city. This was achieved by the following SQL query:
  
SELECT  city, AVG(CAST("productQuantity" as integer)) As averageorders
FROM all_sessions
WHERE "productQuantity" IS NOT NULL 
AND city != 'not available in demo dataset' 
AND city != '(no set)'
GROUP BY city
ORDER BY averageorders DESC

## Results
(fill in what you discovered this data could tell you and how you used the data to answer those questions)

- Finding patterns in product categories: The following code was used to come up with underlying conclusion:
  
product categories according to the country
  
SELECT country, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
ORDER BY "productQuantity"

 --observations--
	 --* Spain and United States are outliers compared to other countries
	 --* buyers bought specific products in larger quantities in these countries

product categories according to the city

SELECT city, "productQuantity", "v2ProductName"
FROM all_sessions
WHERE "productQuantity" IS NOT NULL
AND city != 'not available in demo dataset'
AND city != '(not set)' 
ORDER BY "productQuantity"

--observations--
	 --* Madrid and USA cities are outliers outlier
	 --* Specific products were bought in larger quantities in these cities 
	 -- compared to others (Madrid, Atlanta, Salem)
  
## Challenges 
(discuss challenges you faced in the project)

* Unmastered concepts such as CTEs, Ranks and Window Functions
  
When I reached out to the mentor whose explaination showed me that my initial approach was wrong, I figured I needed to apply concepts like CTEs, Ranks, and Window Functions which I have not mastered yet. This was a challenge to complete the fourth question.

* Short time
  
Because most of the time I spent carrying out researche on internet, the time of doing the actual coding was not enough. 

## Future Goals
(what would you do if you had more time?)

* Do enough practice
The most challenge I found was to combine some SQL queries that I already know to solve a question. That is not easy and I strongly believe it is due to less practice so far.

* Keep seeking support from mentors and peers
I can't stress enough how easy it is to understand something when I am being pushed by an actual human being. Carrying out research is good, but I got lost many times. 
