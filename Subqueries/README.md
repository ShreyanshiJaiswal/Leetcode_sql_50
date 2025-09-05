# Subqueries Questions

This file has all the problems from the Subqueries section of SQL50.

### [1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT employee_id
FROM Employees
WHERE salary < 30000
  AND manager_id NOT IN (
      SELECT employee_id 
      FROM Employees
  )
ORDER BY employee_id;
```
## Thought Process

- The question wants employees whose salary is less than 30000.  
- Along with that, their manager should have left the company.  
- If a manager left, their `employee_id` will not be present in the table anymore.  
- So I need to check employees where `manager_id` is not in the list of current `employee_id`s.  
- At the same time, I apply the salary filter `< 30000`.  
- This means only those employees are selected who earn less than 30000 and whose manager is missing from the table.  
- Finally, I order the result by `employee_id` to get the output in proper order.  
