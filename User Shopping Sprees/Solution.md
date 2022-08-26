# Solution
This is a tough task – Let's break down the problem into detailed steps.

## Problem Summary

Create CTE unique_purchases: keep one transaction for each user on each day
Create CTE date_groups: identify dates that belong to the same shopping spree
Assign a rank to each purchase date for each user
Subtract the rank from transaction_date to create date_group
Create CTE shopping_streaks: group by the user_id and date_group. Then, count the records belonging to each date_group to find the lengths of all shopping sprees
Filter on unique users with at least one 3-day streak
To learn more about the logic of calculating spree lengths, click here.

## Detailed Steps

### Step 1: First, let's obtain all the dates where the user purchased items from Amazon. We don't care about the number of purchases per date; we just want to know whether a given date had a purchase or not.
````sql
WITH unique_purchases AS (
SELECT
  user_id, transaction_date
FROM transactions
GROUP BY user_id, transaction_date
)
````
### Step 2: This is the most difficult part of this task. The idea is to create date_groups that aggregate consecutive purchase dates into streaks. To achieve this, we can utilize a window function like RANK or ROW_NUMBER to rank the dates for each user. Note: In this situation, there is no difference between RANK and ROW_NUMBER because transactions are unique.

Now, when we subtract this rank from transaction_date, we obtain the date_groups. To clarify, any transactions within 3 days of each other will be aggregated into the same data group. This concept might be difficult to grasp at first, so please see the simplified example for one user below.

|transaction_date|	rank	|date_group|
|----------------|--------|----------|
|2022-01-01      |	1	    |2021-12-31|
|2022-01-02      |	2	    |2021-12-31|
|2022-01-04      |	3	    |2022-01-01|

As you can see, this logic combines the dates into groups in the date_group column.

Enough theory; let's put this into practice. The ranking metric is currently an integer, but we need to convert it to an interval in order to perform calculations with date-type columns. We can accomplish this by multiplying RANK() OVER (PARTITION BY user_id ORDER BY transaction_date) with interval '1 day'.

Click here to learn more about intervals and date operations in PostgreSQL.

The query should look like this:
````SQL
date_groups AS (
SELECT
  user_id,
  transaction_date - (
  	RANK() OVER (
    	PARTITION BY user_id
        ORDER BY transaction_date)
        * interval '1 day')
AS date_group
FROM unique_purchases
)
````

### Step 3: There are two ways we could proceed:

Either subtract transaction_date from date_group
Or count the rows per user and date group
We'll use the latter approach so that the resulting metric will be an integer instead of an interval. 
For the above example, the query should look like this:
````SQL
shopping_streaks AS (
SELECT
  user_id,
  COUNT(*) AS consecutive_days
FROM date_groups
GROUP BY user_id, date_group
)
````

Its output should be similar to this:

|user_id|	date_group|	consecutive_days|
|-------|-----------|-----------------|
|1      |2021-12-31 |	2               |
|1	    |2022-01-01 |	1               |

### Step 4: Now, all we have left to do is to filter for users with 3 or more consecutive purchases in the main SELECT:
````SQL
SELECT DISTINCT user_id
FROM shopping_streaks
WHERE consecutive_days >=3
Full solution:

WITH unique_purchases AS (
SELECT
  user_id, transaction_date
FROM transactions
GROUP BY user_id, transaction_date
),

date_groups AS (
SELECT
  user_id,
  transaction_date - (
  	RANK() OVER (
    	PARTITION BY user_id
        ORDER BY transaction_date)
        * interval '1 day')
AS date_group
FROM unique_purchases
),

shopping_streaks AS (
SELECT
  user_id,
  COUNT(*) AS consecutive_days
FROM date_groups
GROUP BY user_id,
         date_group
)

SELECT DISTINCT user_id
FROM shopping_streaks
WHERE consecutive_days >= 3;
````
