*This is the same question as problem #4 in the SQL Chapter of Ace the Data Science Interview!*
# Question
Assume you are given the table below for purchasing activity by product type. Write a query to calculate the cumulative purchases for each product type over time in chronological order. Output the transaction date, product type, and the cumulative number of quantities purchased (conveniently abbreviated as cum_purchased).

`total_trans` **Table:**

|Column Name|	Type|
|----|----|
|order_id|	integer|
|product_type|	string|
|quantity	|integer|
|order_date|	datetime|

`total_trans` **Example Input:**

|order_id|	product_type	|quantity|	order_date|
|----|----|----|----|
|213824	|printer|	20|	06/27/2022 12:00:00|
|212312	|hair dryer|	5	|06/28/2022 12:00:00|
|132842	|printer|	18|	06/28/2022 12:00:00|
|284730	|standing lamp|	8	|07/05/2022 12:00:00|

**Example Output:**

|order_date|	product_type|	cum_purchased|
|----|----|-----|
|06/27/2022 |12:00:00|	printer	|20|
|06/28/2022| 12:00:00	|hair dryer|	5|
|06/28/2022 |12:00:00	|printer	|38|
|07/05/2022| 12:00:00|	standing lamp|	8|

**Explanation**

Over the course of June 27, 2022, 20 printers were purchased. Over the course of June 28, 2022, 5 hair dryers were purchased.
