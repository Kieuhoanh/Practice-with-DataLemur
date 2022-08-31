# Solution
```sql
WITH rank_transaction AS (
SELECT 
product_id
,user_id
,transaction_date
,RANK() OVER(PARTITION BY user_id ORDER BY transaction_date DESC) day_rank
FROM user_transactions
)
SELECT 
transaction_date
,COUNT(DISTINCT user_id) number_of_users
,COUNT(product_id) number_of_products
FROM rank_transaction
WHERE day_rank =1
GROUP BY transaction_date
```
## Answer
|transaction_date	|number_of_users|	number_of_products|
|-----|----|-----|
|07/11/2022 10:00:00	|1|	1|
|07/12/2022 10:00:00|	2|	3|
