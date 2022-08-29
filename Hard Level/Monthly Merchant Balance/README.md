# Question
Say you have access to all the transactions for a given merchant account. Write a query to print the cumulative balance of the merchant account at the end of each day, with the total balance reset back to zero at the end of the month. Output the transaction date and cumulative balance.

`transactions` __Table:__
|Column Name|	Type|
|---|---|
|transaction_id|	integer|
|type|	string ('deposit', 'withdrawal')|
|amount	|decimal|
transaction_date|	timestamp|

`transactions` __Example Input:__
|transaction_id|	type|	amount|	transaction_date|
|---|---|---|---|
|19153|	deposit|	65.90|	07/10/2022 10:00:00|
|53151|	deposit|	178.55|	07/08/2022 10:00:00|
|29776|	withdrawal|	25.90|	07/08/2022 10:00:00|
|16461|	withdrawal|	45.99|	07/08/2022 10:00:00|
|77134|	deposit|	32.60|	07/10/2022 10:00:00|

__Example Output:__
|transaction_date|	balance|
|----|---|
|07/08/2022 12:00:00|	106.66|
|07/10/2022 12:00:00|	205.16|

To get cumulative balance of 106.66 on 07/08/2022 12:00:00, we take the deposit of 178.55 and minus against two withdrawals 25.90 and 45.99.
