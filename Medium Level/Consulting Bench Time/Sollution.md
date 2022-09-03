# Solution
```sql
SELECT 
s.employee_id
,365-sum(c.end_date-c.start_date+1) bench_days
FROM staffing s
LEFT JOIN consulting_engagements c ON c.job_id=s.job_id
WHERE s.is_consultant ='true' AND DATE_PART('YEAR',c.start_date)=2021 
AND DATE_PART('YEAR',c.end_date)=2021
GROUP BY 1
```
## Answer
|employee_id	|bench_days
|----|----|
|111|	222|
|156|	238|
