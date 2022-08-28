# Solution
```sql
WITH sum_demand AS(
SELECT 
datacenter_id
,SUM(monthly_demand) sum_demand
FROM forecasted_demand
GROUP BY datacenter_id
)
SELECT
s.datacenter_id
,(d.monthly_capacity - s.sum_demand) AS spare_capacity
FROM sum_demand s
INNER JOIN datacenters d ON d.datacenter_id=s.datacenter_id
ORDER BY datacenter_id,spare_capacity
```
## Answer
|datacenter_id|	spare_capacity|
|---|----|
|1|	22|
|2|	55|
|3|	12|
|4|	150|
