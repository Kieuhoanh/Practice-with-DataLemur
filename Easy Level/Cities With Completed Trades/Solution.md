# Solution
```sql
SELECT 
u.city
,COUNT(*) AS total_orders
FROM trades t
INNER JOIN users u ON u.user_id=t.user_id
WHERE t.status ='Completed'
GROUP BY u.city
ORDER BY total_orders DESC
LIMIT 3
```
## Answer:
|city|	orders|
|----|-----|
|San Francisco|	4|
|Boston	|3|
|Denver|	2|
