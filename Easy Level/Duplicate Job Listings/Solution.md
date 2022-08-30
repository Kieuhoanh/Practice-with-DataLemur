# Solution
```sql
WITH duplicate AS(
SELECT 
company_id
,title
,description
,COUNT(job_id)
FROM job_listings t1
GROUP BY 1,2,3
HAVING COUNT(job_id) >1
)
SELECT 
COUNT (*) duplicate_companies
FROM duplicate
```

## Answer
|duplicate_companies|
|---|
|3|
