# Solution
To get the ordering of the customer purchases, we can use the ROW_NUMBER window function to get the ordering of customer purchases.

Then, we can use the common table expression (CTE) or subquery to filter customers whose first purchase (denoted as row_num = 1) and is valued at 50 dollars or more (denoted as spend >= 50). Note that this would require the CTE or subquery to include spend also.

```sql
WITH rank_date AS(
SELECT 
user_id
,spend
,transaction_date
,RANK() OVER(PARTITION BY user_id ORDER BY transaction_date) rk
FROM user_transactions
)
SELECT
COUNT(DISTINCT user_id) users
FROM rank_date
WHERE rk=1 AND spend>=50
```
## Answer

|users|
|-----|
3||
