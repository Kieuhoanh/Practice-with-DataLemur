# Question
Facebook wants to create a new algorithm of friend recommendations based on people who are showing interest in attending 2 or more of the same private events. A user interested in attending would have either 'going' or 'maybe' as their attendance status.

Note that friend recommendations are unidirectional, meaning if user x and user y should be recommended to each other, the result table should have both user x recommended to user y and user y recommended to user x.

Also, note that the result table should not contain duplicates (i.e., user y should not be recommended to user x multiple times).

Return the results in user_a, user_b order.

📌`friendship_status` __Table__:
|Column Name|	Type|
|---|----|
|user_a_id	|integer|
|user_b_id	|integer|
|status|	enum ('friends', 'not_friends')|

Each row of this table indicates the status of the friendship between user_a_id and user_b_id.

📌`friendship_status` __Example Input__:
|user_a_id|	user_b_id|	status|
|---|---|----|
|111|	333|	not_friends|
|222|	333|	not_friends|
|333|	222|	not_friends|
|222|	111|	friends|
|111|	222	|friends|
|333|	111|	not_friends|

📌`event_rsvp` __Table__:
|Column Name|	Type|
|---|---|
|user_id|	integer|
|event_id|	integer|
|event_type|	enum ('public', 'private')|
|attendance_status|	enum ('going', 'maybe', 'not_going')|
|event_date|	date|

📌`event_rsvp` __Example Input__:
|user_id|	event_id|	event_type|	attendance_status|	event_date|
|---|---|---|----|---|
|111|	567|	public|	going|	07/12/2022|
|222|	789|	private|	going|	07/15/2022|
|333|	789|	private|	maybe|	07/15/2022|
|111|	234|	private|	not_going	|07/18/2022|
|222|	234|	private	|going|	07/18/2022|
|333|	234|	private|	going|	07/18/2022|

## Example Output:
|user_a_id|	user_b_id|
|----|----|
|222|	333|
|333|	222|

🌟User 222 and 333 who are not friends have showed the same interest in attending 2 or more private events.
