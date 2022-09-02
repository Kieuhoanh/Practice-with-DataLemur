# Solution
```sql
WITH song_appearances AS(
SELECT 
s.artist_id
,COUNT(rank) song_appearances
FROM global_song_rank r
LEFT JOIN songs s ON s.song_id=r.song_id
WHERE rank <11
GROUP BY s.artist_id
)
,artist_rank AS( 
SELECT 
a.artist_name
,DENSE_RANK() OVER(ORDER BY s.song_appearances DESC) artist_rank
FROM song_appearances s
LEFT JOIN artists a ON a.artist_id=s.artist_id
)
SELECT
artist_name
,artist_rank
FROM artist_rank
WHERE artist_rank<=5
ORDER BY 2,1
```
## Answer
|artist_name	|artist_rank|
|-------|-------|
|Bad Bunny|	1|
|Ed Sheeran|	2|
|Adele|	3|
|Lady Gaga|	3|
|Katy Perry|	4|
|Drake|	5|
