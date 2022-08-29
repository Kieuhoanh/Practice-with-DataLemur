# Solution
The first step is to determine the query logic for when the two sessions are concurrent.

Let's say we have two sessions, session 1 and session 2. Note that there are two cases in which they overlap:

1. If session 1 starts first, then the start time for session 2 is less than or equal to session 1’s end time.
2. If session 2 starts first, then session 1’s end time for session 1 is greater than or equal to session 2’s start time.
When we combine both cases, this simplifies to session 2’s start time falling between session 1’s start time and session 1’s end time.
```sql
SELECT
  sessions_1.session_id,
  sessions_2.session_id
FROM sessions AS sessions_1
JOIN sessions AS sessions_2
  ON sessions_1.session_id != sessions_2.session_id
  AND sessions_2.start_time BETWEEN sessions_1.start_time
  AND sessions_1.end_time;
  ```
Here we explain our reasonings for having the two conditions in join:

- First condition sessions_1.session_id != sessions_2.session_id: While we are looking for concurrent sessions, we also do not want sessions where session 1 starts the exact same time as sessions 2.
- Second condition sessions_2.start_time BETWEEN sessions_1.start_time AND sessions_1.end_time: Interpreted as the combination of the two cases in the explanation above where session 2's start time falls in between session 1's start time and end time, or vice versa.
With this in mind, we can move on to finding the number of concurrent session for each session id.
```sql
SELECT
  sessions_1.session_id,
  COUNT(sessions_2.session_id) AS concurrent_sessions
FROM sessions AS sessions_1
JOIN sessions AS sessions_2
  ON sessions_1.session_id != sessions_2.session_id
  AND sessions_2.start_time BETWEEN sessions_1.start_time
  AND sessions_1.end_time
GROUP BY sessions_1.session_id;
```
__Results:__

|session_id	|concurrent_sessions|
|----|----|
|543613|	2|
|242566|	3|
|143256|	1|
|374756|	1|
|746382|	2|
