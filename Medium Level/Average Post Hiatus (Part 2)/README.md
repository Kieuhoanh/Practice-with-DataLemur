# Question

You are given a table of Facebook posts from users who posted at least twice in 2021. Write a query to find the average number of days (with decimals) between each user’s posts during 2021. Output the user and the average number of the days they waited between posts.

## Assumptions

A single user can post several times per day
When calculating differences between dates, output the component of the time interval representing days
**Example output:** 5.5 days
`posts` **Table:**

|Column Name|	Type|
|-----|----|
|user_id	|integer|
|post_id|	integer|
|post_date	|timestamp|
|post_conten|	timestamp|

`posts Example` **Input:**

|user_id	|post_id	|post_date|	post_content|
|----|--|-----|-----|
|151652|	599415|	07/10/2021 12:00:00	|Need a hug|
|151652|	994156|	07/15/2021 12:00:00|	Does anyone have an extra iPhone charger to sell?|
|661093	|624356|	07/29/2021 13:00:00	|Bed. Class 8-12. Work 12-3. Gym 3-5 or 6. Then class 6-10. Another day that's gonna fly by. I miss my girlfriend|
|004239	|784254|	07/04/2021 11:00:00|	Happy 4th of July!|
|661093	|442560	|07/08/2021 14:00:00	|Just going to cry myself to sleep after watching Marley and Me.|
|151652	|111766|	07/12/2021 19:00:00	|I'm so done with covid - need travelling ASAP!|

**Example Output:**

|user_id|	days_between|
|-----|----|
|151652|	2.5|
|661093|	21|

**Explanation:** User 661903 had 2 days between the first and the second post; and 3 days between the second and the third post. Thus, the average is 2.5.
