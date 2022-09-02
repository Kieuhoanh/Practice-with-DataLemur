# Solution
```sql
SELECT 
DATE_PART('MONTH',submit_date) month_submit
,product_id product
,ROUND(AVG(stars),2) avg_stars
FROM reviews
GROUP BY month_submit,product_id
ORDER BY 1,2
```

## Answer
|month_submit|product|	avg_stars|
|-----|-----|---|
|5|	25255|	4.00|
|5|	25600|	4.33|
|6|	12580|	4.50|
|6|	50001|	3.50|
|6|	69852|	4.00|
|7|	11223|	5.00|
|7|	69852|	2.50|
