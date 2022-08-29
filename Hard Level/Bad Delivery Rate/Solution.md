# 🌈Solution
This is a multi-step approach, so let's break it down into piecemeal.

## First, we identify the points requiring our attention:

- We only want customers who signed up in June 2022.
- We only want orders made within the first 14 days from customers' signup date.
- We only want orders with status of 'completed incorrectly' and 'never received'.
- We want orders with actual delivery times later than the estimated delivery times because these orders signify late orders and contribute to the bad experience rating.
- We want orders with NULL actual delivery times because these orders failed to be delivered.
## Based on these points, here's our action plan:

1. Join customers and orders tables based on related column user_id. Then, filter it to the customers' signup_date in June 2022 and ensure that the orders made are between customer's signup_date and customer's signup_date + 14 days. This table represents the orders within the first 14 days made by customers who signed up in June 2022.
2. Subsequently, we wrap the codes in #1 in a common table expression (CTE) or subquery and join with trips table based on a foreign key, trip_id.
3. Next, we filter this newly joined table with order status of 'completed incorrectly' and 'never received' because we only want orders with bad experiences.
4. Then, we filter for cases where the actual_delivery_timestamp is more than estimated_delivery_timestamp because it means that the orders were delivered later than the promised 30 minutes.
5. Filter for when the actual_delivery_timestamp IS NULL to include orders that failed to be delivered to the customers.

Once we're done with the above, we can get on with calculating the percentage of bad experience using this formula.

__Percentage of bad experience: Orders with bad experience from customers who signed up in June 2022 / Total orders made by customers who signed up in June 2022__

To get "Orders with bad experience from customers who signed up in June 2022", we can simply take the count of user_id since we already filtered out the irrelevant orders and customers who signed up in other months.

As for "Total orders made by users who signed up in June 2022", we take the count of total orders in june22_orders CTE because this table contains all the orders made by customers in June 2022 and within the first 14 days from signup date.

With that, we wrap the formula with ROUND( ,2) function to round the percentage to 2 decimal places.
````sql
WITH june22_orders 
AS (
SELECT 
  orders.order_id,
  orders.trip_id,
  orders.status
FROM customers
JOIN orders
  ON customers.customer_id = orders.customer_id
WHERE EXTRACT(MONTH FROM customers.signup_timestamp) = 6
  AND EXTRACT(YEAR FROM customers.signup_timestamp) = 2022
  AND customers.signup_timestamp + interval '14 days' > orders.order_timestamp)

SELECT ROUND(100.0 * COUNT(june22.order_id)/
  (SELECT COUNT(order_id) FROM june22_orders),2) AS bad_experience_pct
FROM june22_orders AS june22
JOIN trips
  ON june22.trip_id = trips.trip_id
WHERE june22.status IN ('completed incorrectly', 'never received')
  OR trips.actual_delivery_timestamp IS NULL 
  AND trips.estimated_delivery_timestamp > trips.actual_delivery_timestamp;
SELECT * FROM orders;
````

