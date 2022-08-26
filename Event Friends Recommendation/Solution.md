# Solution
Let's create a common table expression (CTE) to find the distinct users that are attending two or more private events.

Using the `HAVING` clause, we can filter to how many of the qualifying private events the user is interested in attending, which in this case means 2 or more events.
```sql
SELECT DISTINCT user_id
FROM event_rsvp
WHERE attendance_status <> 'not_going'
  AND event_type = 'private'
GROUP BY user_id
HAVING COUNT(event_type) > 1;
```
Output is showing users who are attending 2 or more private events:

|user_id|
|---|
|222|
|333|
|444|

Now, we can convert the query into a CTE called user_events and join to the friendship_status table to find other users who are not friends, but are also attending the same events.

The `EXISTS` clause will help us join back to the user_events CTE to know which friend recommended users are attending the same events.
```sql
WITH user_events
AS (
-- Insert query above)

SELECT friends.user_a_id, friends.user_b_id
FROM friendship_status AS friends
JOIN user_events AS events
  ON events.user_id = friends.user_a_id
  AND friends.status = 'not_friends'
  AND EXISTS (
    SELECT 1
    FROM user_events AS events_2
    WHERE events_2.user_id = friends.user_b_id)
ORDER BY friends.user_a_id, friends.user_b_id;
```
Results:

|user_a_id|	user_b_id|
|---|---|
|222|	333|
|333|	444|

Solution:
```SQL
WITH user_events
AS (
SELECT DISTINCT user_id
FROM event_rsvp
WHERE attendance_status <> 'not_going'
  AND event_type = 'private'
GROUP BY user_id
HAVING COUNT(event_type) > 1)

SELECT
  friends.user_a_id, friends.user_b_id
FROM friendship_status AS friends
JOIN user_events AS events
  ON events.user_id = friends.user_a_id
  AND friends.status = 'not_friends'
  AND EXISTS (
    SELECT 1
    FROM user_events AS events_2
    WHERE events_2.user_id = friends.user_b_id)
ORDER BY friends.user_a_id, friends.user_b_id;
```
