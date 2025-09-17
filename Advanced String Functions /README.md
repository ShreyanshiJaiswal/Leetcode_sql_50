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

### [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT patient_id, patient_name, conditions 
FROM Patients
WHERE conditions LIKE 'DIAB1%' 
   OR conditions LIKE '% DIAB1%';
```
## Thought Process
- We need to find all patients whose conditions include `"DIAB1"`.  
- Sometimes `"DIAB1"` can appear at the very beginning of the string, so we check with `LIKE 'DIAB1%'`.  
- Other times, it can appear after a space (not at the start), so we also check with `LIKE '% DIAB1%'`.  
- Using `OR` ensures we capture both cases.  
- Finally, select the required columns: `patient_id`, `patient_name`, and `conditions`.  

### [196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
DELETE FROM Person
WHERE id NOT IN (
    SELECT id
    FROM (
        SELECT MIN(id) AS id
        FROM Person
        GROUP BY email
    ) AS t
);
```
## Thought Process
- The goal is to **remove duplicate emails** but keep only one record for each email.  
- Use `GROUP BY email` to group records with the same email.  
- Within each group, keep the record with the smallest `id` using `MIN(id)`.  
- Subquery returns only these valid `id`s to keep.  
- Delete all rows in `Person` where `id` is **not in** this list.  
- Wrapping the grouped subquery in another derived table (`AS t`) avoids MySQL’s restriction on modifying and selecting from the same table simultaneously.  
