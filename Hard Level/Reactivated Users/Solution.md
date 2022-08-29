# Solution
Before we proceed with the solution, let's understand what is a Reactivated User.

__Reactivated users are dormant users who did not log in the previous month, who then logged in the following month.__

We'll use a multi-step approach to solve this:

1. First, find the users who login in the previous month.
2. Then, find the users who login in the current month.
3. In the final query, we will find for the users who login in the current month, then using a `NOT EXISTS` operator, we will exclude users who exist in the previous month's login data.
In the first step, we look at all the users who login during the previous month. To obtain the last month’s data, we subtract an `INTERVAL` of 1 month from the current month’s login date.

Then, we use a `NOT EXISTS` against previous month’s login information to check whether there was a login in the previous month. If there is a login in the previous month, then the `NOT EXISTS` operator excludes this particular user.

Finally, we `COUNT` the number of users satisfying this condition.
```sql
SELECT 
  EXTRACT(MONTH FROM curr_month.login_date) AS current_month, 
  COUNT(curr_month.user_id) AS reactivated_users
FROM user_logins AS curr_month 
WHERE 
  NOT EXISTS (
    SELECT * 
    FROM user_logins AS last_month 
    WHERE curr_month.user_id = last_month.user_id 
      AND EXTRACT(MONTH FROM last_month.login_date) = (
        EXTRACT(MONTH FROM curr_month.login_date - '1 month' :: INTERVAL))
) 
GROUP BY EXTRACT(MONTH FROM curr_month.login_date)
ORDER BY current_month ASC;
```
