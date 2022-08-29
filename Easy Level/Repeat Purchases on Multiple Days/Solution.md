# Solution
```sql
WITH solution AS (
SELECT 
user_id
,product_id
,COUNT (DISTINCT DATE(purchase_date)) count_purchase
FROM purchases
GROUP BY user_id,product_id
HAVING COUNT (DISTINCT DATE(purchase_date)) >=2
)
SELECT
COUNT (*) users_num
FROM solution
```

## Answer
|users_num|
|1|
