# Solution
``` sql
SELECT
profile_id
FROM personal_profiles p
LEFT JOIN company_pages c ON c.company_id=p.employer_id
WHERE  p.followers>c.followers
```

## Answer
|profile_id|
|--|
|1|
|3|
|4|
|5|
|7|
