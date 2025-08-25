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

### [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT 
    activity_date AS day,
    COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN DATE('2019-06-28') AND DATE('2019-07-27')
GROUP BY activity_date;
```
## Thought Process
- The task is to find the **number of active users per day** in the past 30 days.  
- Since multiple activities by the same user on the same day shouldn’t be double counted, use `COUNT(DISTINCT user_id)`.  
- We only consider dates between `'2019-06-28'` and `'2019-07-27'`.  
- `GROUP BY activity_date` ensures results are calculated **per day**.  
- Aliased `activity_date` as `day` for clarity in output.
