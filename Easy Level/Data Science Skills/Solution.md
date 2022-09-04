# Solution
```sql
SELECT 
candidate_id
FROM candidates
GROUP BY 1
HAVING SUM(case when skill in ('Python', 'Tableau', 'PostgreSQL') then 1 else 0 end) = 3
ORDER BY 1 
```
## Answer
|candidate_id|
|-------|
|123|
|147|
