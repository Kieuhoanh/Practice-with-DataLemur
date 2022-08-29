# 🏆Solution
## 🥇Step 1:

First, we merge the advertiser and daily_pay tables with LEFT JOIN.
````sql
SELECT
  advertiser.user_id,
  advertiser.status,
  payment.paid
FROM advertiser
LEFT JOIN daily_pay AS payment
  ON advertiser.user_id = payment.user_id
````
Showing first 5 rows out of 8 rows:

|user_id|	status|	paid|
|----|---|---|
|bing|	NEW	| |
|yahoo|	NEW|	45.00|
|alibaba	|EXISTING	|100.00|
|baidu|	EXISTING	| |
|target|	CHURN|	13.00|

Do you know why we're joining the tables using LEFT JOIN instead of (INNER) JOIN?

Say, if we use JOIN instead, this is the output we'll get:

|user_id|	status|	paid|
|----|---|----|
|yahoo|	NEW|	45.00|
|alibaba|	EXISTING|	100.00|
|target|	CHURN|	13.00|

Bing and Baidu is no longer in the output because they have not made any payment yet and do not exist in the daily_pay table. Since the question wants us to tag their payment status regardless of payment made, we have to ensure that we gather all the advertisers' payment information.

## 🥈Step 2:

Did you realise that one of the advertiser is missing from the table? If you query SELECT * FROM daily_pay, you will notice that Fitdata is missing. That's because Fitdata is a new advertiser and its data is not reflected in the advertiser table yet.

To ensure that we have a complete table with all the existing and new advertisers, we have to merge both tables vertically.

After this, we LEFT JOIN daily_pay with advertiser. This will let us know which users are new. At last, we join the results produced by these two left joins using UNION. If paid is null, then that user have not paid at day t and if status is null then the user is a new user(who's information is not present in advertiser table but that user paid on day t, so this particular user is called as new user)

A graphical presentation of how the UNION looks:
````sql
SELECT ...
FROM advertiser
LEFT JOIN daily_pay -- Find out who pay and did not pay
UNION
SELECT ...
FROM daily_pay
LEFT JOIN advertiser -- Find out if there's new paid user
````
And, how the complete query looks:
````sql
SELECT
  advertiser.user_id,
  advertiser.status,
  payment.paid
FROM advertiser
LEFT JOIN daily_pay AS payment
  ON advertiser.user_id = payment.user_id
UNION
SELECT
  payment.user_id,
  advertiser.status,
  payment.paid
FROM daily_pay AS payment
LEFT JOIN advertiser
  ON advertiser.user_id = payment.user_id
  ````
Bear in mind that the second query has the daily_pay table being the left table as Fitdata advertiser is sitting in this table.

Now you should have the complete table with 9 rows:

|user_id|	status|	paid|
|----|----|----|
|fitdata| |		25.00|
|baidu|	EXISTING	| |
|morgan|	RESURRECT|	600.00|
|target|	CHURN	|13.00|
|alibaba|	EXISTING	|100.00|

Interpreting this table based on the transitions table:

- Fitdata is a new advertiser who has paid $25 with its new status being NEW.
- Baidu and Alibaba are existing advertisers, but only Alibaba has made a payment and remains as EXISTING whereas Baidu is CHURN.
- Since Morgan has made a payment, its new status will be changed to EXISTING.
- Target's CHURN status will be changed to RESURRECT.

## 🥉Step 3:

Our final step is to assign each advertiser to its new status using a conditional CASE statement based on the payment conditions set out:

- New: users registered and made their first payment.
- Existing: users who paid previously and recently made a current payment.
- Churn: users who paid previously, but have yet to make any recent payment.
- Resurrect: users who did not pay recently but may have made a previous payment and have made payment again recently.
````sql
WITH payment_status
AS (
-- Insert query in step 2)

SELECT
  user_id,
  CASE WHEN paid IS NULL THEN 'CHURN'
    WHEN status != 'CHURN' AND paid IS NOT NULL THEN 'EXISTING'
    WHEN status = 'CHURN' AND paid IS NOT NULL THEN 'RESURRECT'
    WHEN status IS NULL THEN 'NEW'
  END AS new_status
FROM payment_status;
````
Results:

|user_id|	new_status|
|---|----|
|fitdata|	NEW|
|baidu|	CHURN|
|morgan	|EXISTING|
|target|	RESURRECT|
|alibaba	|EXISTING|

Solution:
````sql
WITH payment_status
AS (SELECT
advertiser.user_id,
advertiser.status,
payment.paid
FROM advertiser
LEFT JOIN daily_pay AS payment
ON advertiser.user_id = payment.user_id
UNION
SELECT
payment.user_id,
advertiser.status,
payment.paid
FROM daily_pay AS payment
LEFT JOIN advertiser
ON advertiser.user_id = payment.user_id)

SELECT
user_id,
CASE
  WHEN paid IS NULL THEN 'CHURN' 
  WHEN status != 'CHURN' AND paid IS NOT NULL THEN 'EXISTING'
  WHEN status = 'CHURN' AND paid IS NOT NULL THEN 'RESURRECT'
  WHEN status IS NULL THEN 'NEW'
END AS new_status
FROM payment_status;
````
