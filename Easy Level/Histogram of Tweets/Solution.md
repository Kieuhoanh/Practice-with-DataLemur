# Solution
```sql
WITH num_tweet_per_user AS(
SELECT 
user_id
,COUNT(tweet_id) tweet_bucket
FROM tweets
WHERE DATE_PART('year',tweet_date)=2022
GROUP BY user_id )
SELECT
tweet_bucket
,COUNT (user_id) users_num
FROM num_tweet_per_user
GROUP BY tweet_bucket
```
## Answer
|tweet_bucket|	users_num|
|------|------|
|1|	2|
|2	|1|
