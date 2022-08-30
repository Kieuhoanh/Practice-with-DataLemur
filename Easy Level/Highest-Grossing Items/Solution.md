# Solution
```sql
WITH total_spend AS(
SELECT
category
,product
,SUM(spend) total_spend
FROM product_spend 
WHERE DATE_PART('year',transaction_date)=2022
GROUP BY category,product
)
,rank_spend AS(
SELECT 
category
,product
,total_spend
,RANK () OVER(PARTITION BY category ORDER BY total_spend DESC) rk
FROM total_spend
)
SELECT
category
,product
,total_spend
FROM rank_spend
WHERE rk in (1,2)
```

## Answer
|category|	product|	total_spend|
|----|------|-------|
|appliance|	washing machine|	439.80|
|appliance	|refrigerator	|299.99|
|electronics|	vacuum|	486.66|
|electronics|	wireless headset|	447.90|
