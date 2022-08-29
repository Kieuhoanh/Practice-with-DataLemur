# Question
This is the same question as problem #31 in the SQL Chapter of Ace the Data Science Interview!

Assume you are given the table below containing information on Facebook user logins. Write a query to obtain the number of reactivated users (which are dormant users who did not log in the previous month, then logged in during the current month).

Output the current month (in numerical) and number of reactivated users.

## Assumption:

- The rows in user_logins table is complete for the year of 2022 and there are no missing dates.

📌`user_logins` __Table:__

|Column Name|	Type|
|---|---|
|user_id|	integer|
|login_date|	datetime|

📌`user_logins`__Table:__
|user_id|	login_date|
|----|----|
|725|	03/03/2022 12:00:00|
|245|	03/28/2022 12:00:00|
|112|	03/05/2022 12:00:00|
|245|	04/29/2022 12:00:00|
|112|	04/05/2022 12:00:00|

Assume that the above table is complete for month of February to April 2022.

__Example Output:__
|current_month|	reactivated_users|
|---|---|
|3	|3|

In March 2022, there are 3 reactivated users which are 725, 245, and 112. These 3 users did not login in February 2022, but login in the current month in March 2022.

There are no reactivated users in April because users 245 and 112 login in the previous month in March 2022 and the current month in April, thus they are not reactivated users.
