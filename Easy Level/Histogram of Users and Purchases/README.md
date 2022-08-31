*This is the same question as problem #13 in the SQL Chapter of Ace the Data Science Interview!*
# Question
Assume you are given the below table on transactions from users. Bucketing users based on their latest transaction date, write a query to obtain the number of users who made a purchase and the total number of products bought for each transaction date. Output the transaction date, number of users and number of products.

`user_transactions` **Table:**

|Column Name|	Type|
|-----|----|
|product_id|	integer|
|user_id|	integer|
|spend	|decimal|
|transaction_date|	timestamp|

`user_transactions` **Example Input:**

|product_id	|user_id	|spend|	transaction_date|
|----|------|----|-----|
|3673|	123|	68.90	|07/08/2022 12:00:00|
|9623	|123|	274.10|	07/08/2022 12:00:00|
|1467	|115	|19.90|	07/08/2022 12:00:00|
|2513|	159	|25.00	|07/08/2022 12:00:00|
|1452|	159|	74.50|	07/10/2022 12:00:00|

**Example Output:**

|transaction_date	|number_of_users|	number_of_products|
|------|-----|-----|
|07/08/2022 |12:00:00	|2|	2|
|07/10/2022| 12:00:00|	1	|1|
