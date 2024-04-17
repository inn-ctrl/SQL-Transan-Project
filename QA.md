What are your risk areas? Identify and describe them.

* Miscalculations

QA Process:
Describe your QA process and include the SQL queries used to execute it.

* I carried a filtering search to find a mismatch. There is a city mismatching a country in all_sessions table. New York corrosesponding to Canada instead of United States.
* To confirm that inconsistency, I used this query:

SELECT * 
FROM all_sessions
WHERE city = 'New York' AND country = 'Canada'

* I solved that using the following SQL query:
  
UPDATE all_sessions
SET country = 'United States'
WHERE city = 'New York' AND country = 'Canada';

* To confirm that it is solved I run this query again to make sure it returns nothing, and it did:
  
SELECT * 
FROM all_sessions
WHERE city = 'New York' AND country = 'Canada'
