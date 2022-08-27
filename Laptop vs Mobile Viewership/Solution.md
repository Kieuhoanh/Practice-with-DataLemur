# Solution
```sql
SELECT
SUM(CASE WHEN device_type='laptop' then 1 end) laptop_views
,SUM(CASE WHEN device_type in ('phone' ,'tablet') then 1 end) mobile_views
FROM viewership
```
## Answer
|laptop_views|	mobile_views|
|-----|----|
|2	|3|
