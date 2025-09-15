# Advanced String Functions Questions

This file has all the problems from the Advanced String Functions section of SQL50.

### [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT 
    user_id,
    CONCAT(
        UPPER(SUBSTRING(name, 1, 1)), 
        LOWER(SUBSTRING(name, 2))
    ) AS name
FROM Users
ORDER BY user_id;
```
## Thought Process
- The problem is about fixing the formatting of names in the table.  
- Each name should start with an uppercase letter and the rest should be lowercase.  
- To achieve this, we can take the first character of the name using `SUBSTRING(name, 1, 1)` and convert it to uppercase with `UPPER()`.  
- For the remaining characters, use `SUBSTRING(name, 2)` and convert them to lowercase with `LOWER()`.  
- Combine both parts using `CONCAT()` to form the corrected name.  
- Finally, order the output by `user_id` for a consistent result.  
