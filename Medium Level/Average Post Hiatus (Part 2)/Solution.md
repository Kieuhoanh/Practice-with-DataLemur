# Solution
```sql
SELECT user_id 
,DATE_PART('DAY', MAX(post_date)-MIN(post_date)) / (COUNT(post_id)-1) as days_between
FROM posts
WHERE DATE_PART('year', post_date::DATE) = 2021
GROUP BY user_id
HAVING COUNT(post_id) >= 2;
```
## Answer
|user_id|	days_between|
|----|-----|
|151652|	153.5|
|661093	|102.5|
