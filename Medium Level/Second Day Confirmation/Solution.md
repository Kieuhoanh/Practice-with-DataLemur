# Solution
```sql
ELECT 
e.user_id
FROM emails e
INNER JOIN texts t ON t.email_id=e.email_id
AND t.signup_action ='Confirmed' AND e.signup_date + INTERVAL '1 DAY' = t.action_date
```
## Answer
|user_id|
|----|
|1052|
|1235|
