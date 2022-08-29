# Solution
```sql
SELECT page_id from pages
EXCEPT
SELECT page_id from page_likes
ORDER BY page_id
```

## Anwer:
|page_id|
|---|
|20701|
|32728|
