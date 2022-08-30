# Solution
```sql
WITH num_transactions AS(
SELECT
*
,ROW_NUMBER() OVER(PARTITION BY user_id ORDER BY transaction_date) rk
FROM transactions
)
SELECT 
user_id
,spend
,transaction_date
FROM num_transactions
WHERE rk=3
```
## Answer
|user_id	|spend	|transaction_date|
|------|----|----|
|111	|89.60|	02/05/2022 12:00:00|
|121|	67.90|	04/03/2022 12:00:00|
|263|	100.00	|07/12/2022 12:00:00|
