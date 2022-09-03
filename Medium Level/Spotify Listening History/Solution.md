# Solution
```sql
WITH cte AS(
SELECT 
user_id
,song_id
,COUNT(listen_time) song_plays
FROM songs_weekly
WHERE listen_time< '08/05/2022'
GROUP BY user_id,song_id
UNION ALL
SELECT
user_id
,song_id
,song_plays
FROM songs_history h  )

SELECT
user_id
,song_id
,SUM(song_plays) song_plays
FROM cte
GROUP BY user_id,song_id
ORDER BY song_plays DESC
```
## Answer
|user_id	|song_id|	song_plays|
|----|----|----|
|105|	4520	|25|
|785	|4123	|21|
|777	|1238	|12|
|695	|1238	|10|
|125	|9630	|3|
|695	|4520	|2|
|105	|1238	|1|
