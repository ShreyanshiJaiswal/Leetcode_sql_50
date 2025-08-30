# Advanced Select and Joins Questions

This file has all the problems from the Basic Advanced Select and Joins section of SQL50.

### [1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT 
    m.employee_id,
    m.name,
    COUNT(e.employee_id) AS reports_count,
    ROUND(AVG(e.age)) AS average_age
FROM Employees e
JOIN Employees m
    ON e.reports_to = m.employee_id
GROUP BY m.employee_id, m.name
ORDER BY m.employee_id;
```
## Thought Process
- Goal: Find how many employees report to each manager and their average age.  
- Step 1: Use a **self-join** on the `Employees` table:  
  - `e` = employee (the one who reports)  
  - `m` = manager (the one being reported to).  
- Step 2: Match with `ON e.reports_to = m.employee_id`.  
- Step 3: For each manager, count how many employees report to them → `COUNT(e.employee_id)`.  
- Step 4: Calculate the average age of these reporting employees → `AVG(e.age)`, rounded with `ROUND()`.  
- Step 5: Group results by `m.employee_id` and `m.name` (since each manager’s summary is required).  
- Step 6: Order by `m.employee_id` for a clean ascending order list.  

📌 This ensures we see each manager, how many direct reports they have, and the average age of their team members.

