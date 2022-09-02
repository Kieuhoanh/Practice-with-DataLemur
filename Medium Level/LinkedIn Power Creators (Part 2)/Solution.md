# Solution 
```sql
WITH company AS(
SELECT
e.personal_profile_id 
,MAX(C.followers) max_follower
FROM employee_company e
LEFT JOIN company_pages c ON c.company_id=e.company_id
GROUP BY e.personal_profile_id
)
SELECT
c.personal_profile_id
FROM company c
LEFT JOIN personal_profiles p ON p.profile_id=c.personal_profile_id
WHERE p.followers>c.max_follower
```
## Answer
|personal_profile_id|
|-----|
|1|
|4|
|5|
|7|
