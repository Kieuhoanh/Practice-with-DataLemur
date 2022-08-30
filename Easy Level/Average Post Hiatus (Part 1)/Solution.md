# Solution
``` sql
SELECT
user_id
,MAX(post_date::date)-MIN(post_date::date) AS days_between
from posts
WHERE DATE_PART('year',post_date)=2021
GROUP BY user_id
HAVING COUNT(post_id)>1
```
## Answer
|user_id	|days_between|
|------|----|
|151652|	307|
|661093|	206|
