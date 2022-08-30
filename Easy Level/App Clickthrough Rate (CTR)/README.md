*This is the same question as problem #1 in the SQL Chapter of Ace the Data Science Interview!*
# Question
Assume you have an events table on app analytics. Write a query to get the click-through rate percentage (CTR %) per app in 2022. Output the results in percentage rounded to 2 decimal places.

Note that to avoid integer division, you should multiple your percentage results by 100.0 and not 100.

p.s. unsure how click-through rates are defined? Just scroll to the bottom to get a lil' hint!
`events` **Table:**
|Column Name|	Type|
|-----|-----|
|app_id	|integer|
|event_type	|string|
|timestamp|	datetime|

`events` **Example Input:**
|app_id	|event_type|	timestamp|
|-------|-------|-------|
|123|	impression|	07/18/2022 11:36:12|
|123|	impression	|07/18/2022 11:37:12|
|123|	click|	07/18/2022 11:37:42|
|234|	impression|	07/18/2022 14:15:12|
|234	|click	|07/18/2022 14:16:12|

**Example Output:**
|app_id|	ctr|
|-------|----|
|123|	50.00|
|234|	100.00|

**Explanation**

App 123 has a CTR of 50% because there was 1 click out of the 2 impressions. App 234 has a CTR of 100%.
