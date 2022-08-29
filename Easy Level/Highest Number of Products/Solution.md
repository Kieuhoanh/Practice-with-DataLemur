# Solution
```sql
SELECT
user_id
,product_num
FROM(
SELECT 
user_id
,COUNT(*) product_num
,SUM(spend) total_spend
FROM user_transactions
GROUP BY user_id
HAVING SUM(spend) >= 1000
ORDER BY 2 DESC, 3 DESC) a
LIMIT 3
```

## Answer
|user_id	|product_num|
|---|----|
|133|	4|
|128|	2|
|173|	1
