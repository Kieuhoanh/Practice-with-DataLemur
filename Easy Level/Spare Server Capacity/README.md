# Question
Microsoft Azure's capacity planning team wants to understand how much data its customers are using, and how much spare capacity is left in each of it's data centers. You’re given three tables: customers, datacenters, and forecasted_demand.

Write a query to find the total monthly unused server capacity for each data center. Output the data center id in ascending order and the total spare capacity.

P.S. If you've read the Ace the Data Science Interview and liked it, consider writing us a review?

`customers` **Table:**

|Column Name|	Type|
|----|----|
|name|	string|
|customer_id	|integer|

`customers` **Example Input:**

|name	|customer_id|
|----|------|
|Florian Simran|	144|
|Esperanza A. Luna|	109|
|Garland Acacia	|852|

`datacenters` **Table:**

|Column Name|	Type|
|-----|----|
|datacenter_id|	integer|
|name|	string|
|monthly_capacity	|integer|

`datacenters` **Example Input:**

|datacenter_id|	name|	monthly_capacity|
|----|-----|-----|
|1|	London|	100|
|3|	Amsterdam	|250|
|4|	Hong Kong	|400|

`forecasted_demand` **Table:**

|Column Name|	Type|
|------|------|
|customer_id|	integer|
|datacenter_id||	integer|
|monthly_demand|	integer|

`forecasted_demand` **Example Input:**

|customer_id|	datacenter_id|	monthly_demand|
|-----|-----|------|
|109|	4|	120|
|144|	3	|60|
|144|	4|	105|
|852|	1	|60|
|852|	3	|178|

**Example Output:**

|datacenter_id|	spare_capacity|
|-------|------|
|1|	40|
|3|	12|
|4|	175|
