# Solution
```sql
SELECT
e.app_id
,ROUND(100.0*SUM(CASE WHEN event_type='click' then 1 else 0 end)/SUM (CASE WHEN event_type='impression' then 1 else 0 end),2) ctr
FROM events e
WHERE DATE_PART('year',timestamp)=2022
GROUP BY e.app_id
```
## Answer
|app_id	|ctr|
|-----|-----|
|123	|66.67|
|234	|33.33|
