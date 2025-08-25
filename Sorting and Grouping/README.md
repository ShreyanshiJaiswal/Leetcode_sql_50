# Sorting and Grouping Questions

This file has all the problems from the Sorting and Grouping section of SQL50. 

### [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT 
    teacher_id, 
    COUNT(DISTINCT subject_id) AS cnt 
FROM Teacher 
GROUP BY teacher_id;
```
## Thought Process
- I need to find how many **different subjects** each teacher teaches.  
- The `DISTINCT subject_id` ensures no duplicate subjects are counted.  
- Use `COUNT(DISTINCT subject_id)` to calculate unique subjects.  
- Apply `GROUP BY teacher_id` so the result is shown per teacher.

