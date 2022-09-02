# Solution
```sql
SELECT 
advertiser_id
,ROUND(((SUM(revenue)/SUM(spend)):: DECIMAL),2) ROAS
FROM ad_campaigns
GROUP BY advertiser_id
ORDER BY advertiser_id
```
## Answer
|advertiser_id|	roas|
|------|-----|
|1|	0.84|
|2|	3.89|
|3|	1.50|
|4|	4.00|
|6|	2.40|
