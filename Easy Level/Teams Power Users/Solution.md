# Solution
```sql
SELECT 
sender_id
,count(message_id) message_count
FROM messages
WHERE DATE_PART('month',sent_date) =8 and DATE_PART('year',sent_date) =2022
GROUP BY sender_id
ORDER BY message_count DESC
LIMIT 2 
```
## Answer
|sender_id|	message_count|
|----|-----|
|3601	|4|
|2520	|3|
