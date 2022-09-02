# Solution
```sql
WITH count_post_rolling AS(
SELECT DISTINCT
user_id
,tweet_date
,COUNT(DISTINCT tweet_id)   tweet_num
FROM tweets
GROUP BY user_id,tweet_date
)
SELECT
user_id
,tweet_date
,ROUND(AVG(tweet_num) OVER(PARTITION BY user_id ORDER BY tweet_date
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW),2) rolling_avg_3days
FROM count_post_rolling
```
## Answer
|user_id	|tweet_date|	rolling_avg_3days|
|------|------|------|
|111|	06/01/2022 04:00:00	|2.00|
|111|	06/02/2022 04:00:00|	1.50|
|111|	06/04/2022 04:00:00	|1.33|
|111|	06/15/2022 04:00:00|	1.00|
|199|	06/08/2022 04:00:00|	2.00|
|199|	06/22/2022 04:00:00	|1.50|
