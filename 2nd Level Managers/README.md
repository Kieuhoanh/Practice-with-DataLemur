# Question:

Assume we have a table of Google employees with their responding managers.

A manager is an employee with a direct report. A 2nd level manager is an employee who manages at least one manager, but none of their direct reports are 2nd level managers themselves. Write a query to find the 2nd level managers and their direct reports.

* Output the manager's name and the count of direct reports.

## Assumptions:

An employee can have two second level managers.<br>

`employees` **Table:**
|Column Name |Type|
|----|----|
|emp_id	|integer|
|manager_id	|integer|
|manager_name	|string|

`employees` **Example Input:**
|emp_id|	manager_id|	manager_name|
|----|----|----|
|1	|101|	Duyen|
|101|	1001|	Rick|
|103|	1001|	Rick|
|1001|	1008|	John|

**Example Output:**
|manager_name|	direct_report_count|
|----|----|
|Rick|	1|

Rick is a second level manager who has one first level manager directly reporting to him, which is employee id 101. Employee 103 is not a first level manager, hence is excluded from the output.
