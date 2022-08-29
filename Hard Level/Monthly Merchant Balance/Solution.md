# Solution
To start off, it is much easier if we start to solve the problem from the end - i.e. we want to have daily cumulative balances that reset every month. Thus, to obtain two different granularities of transaction_date column we can utilize DATE_TRUNC function.

In order to obtain balances instead of solely transaction values, we can use CASE to assign positive sign to deposit and negative to withdrawals, and then just sum and group the values on a daily level (there might be multiple transactions during the day).

As the next step, we utilize SUM with a window function and calculate the sum partitioning by month - this makes sure that the cumulative sum is set to zero each month.
```sql
WITH daily_balances
AS (
  SELECT
    DATE_TRUNC('day', transaction_date) AS transaction_day,
    DATE_TRUNC('month', transaction_date) AS transaction_month,
    SUM(CASE WHEN type = 'deposit' THEN amount
      WHEN type = 'withdrawal' THEN -amount END) AS balance
  FROM transactions
  GROUP BY 1, 2
  ORDER BY 1)

SELECT
  transaction_day,
  SUM(balance) OVER (
    PARTITION BY transaction_month
    ORDER BY transaction_day) AS balance
FROM daily_balances
ORDER BY transaction_day;
```
