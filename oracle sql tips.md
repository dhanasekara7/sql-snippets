```sql

STATION table
CITY column

-- select
-- city name, length big ,small

select *
from
(
SELECT CITY, LENGTH(CITY) FROM STATION
ORDER BY LENGTH(CITY) , CITY
) where ROWNUM <= 1;

select *
from
( SELECT CITY, LENGTH(CITY) FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
) where ROWNUM <= 1;


--SELECT CITY CONTAINS VOWEL
SELECT DISTINCT CITY FROM STATION
WHERE LOWER(SUBSTR(CITY,LENGTH(CITY),1)) IN ('a','e','i','o','u')
AND LOWER(SUBSTR(CITY,0,1)) IN ('a','e','i','o','u');

--Query the list of CITY names from STATION that do not start with vowels and do not end with vowels.
--Your result cannot contain duplicates.
SELECT DISTINCT CITY FROM STATION
WHERE LOWER(SUBSTR(CITY,0,1)) NOT IN ('a','e','i','o','u')
AND
LOWER(SUBSTR(CITY,LENGTH(CITY),1)) NOT IN ('a','e','i','o','u');


```