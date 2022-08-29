# Solution
```sql
SELECT
order_date
,product_type
, SUM(quantity) 
  OVER( PARTITION BY PRODUCT_TYPE ORDER BY ORDER_DATE ASC) AS cum_purchased
FROM total_trans
ORDER BY ORDER_DATE ASC
```
## Answer
|order_date|	product_type|	cum_purchased|
|----|----|----|
|06/27/2022 12:00:00|	printer|	20|
|06/28/2022 12:00:00|	hair dryer	|5|
|06/28/2022 12:00:00|	printer|	38|
|07/05/2022 12:00:00|	standing lamp	|8|
|07/05/2022 12:00:00|	printer	|63|
|07/06/2022 12:00:00|	standing lamp|	44|
