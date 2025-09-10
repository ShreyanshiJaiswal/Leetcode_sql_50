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

### [626. Exchange Seats](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT id,
       CASE 
            WHEN id % 2 = 1 AND id + 1 <= (SELECT MAX(id) FROM Seat)
                THEN (SELECT student FROM Seat s WHERE s.id = Seat.id + 1)
            WHEN id % 2 = 0
                THEN (SELECT student FROM Seat s WHERE s.id = Seat.id - 1)
            ELSE student
       END AS student
FROM Seat
ORDER BY id;
```
## Thought Process
- Swap students in adjacent seats (odd ↔ next, even ↔ previous).  
- If `id` is odd and the next seat exists, take the student from `id + 1`.  
- If `id` is even, take the student from `id - 1`.  
- If last seat is odd with no pair, keep the same student.  
- Use `CASE` and small subqueries to pick the neighbor’s student when swapping.  
- Order by `id` so output follows seat order.

### [1341. Movie Rating](https://leetcode.com/problems/movie-rating/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
(
    SELECT u.name AS results
    FROM Users u
    JOIN (
        SELECT user_id, COUNT(*) AS rating_count 
        FROM MovieRating 
        GROUP BY user_id
    ) r  
    ON u.user_id = r.user_id 
    ORDER BY r.rating_count DESC, u.name ASC
    LIMIT 1
)
UNION ALL
(
    SELECT m.title AS results
    FROM Movies m 
    JOIN (
        SELECT movie_id, AVG(rating) AS avg_rating 
        FROM MovieRating
        WHERE created_at >= '2020-02-01'
          AND created_at < '2020-03-01' 
        GROUP BY movie_id
    ) r 
    ON m.movie_id = r.movie_id
    ORDER BY r.avg_rating DESC, m.title ASC
    LIMIT 1
);
```
## Thought Process
- The question asks for **two results**:  
  1. The user who gave the most ratings.  
  2. The movie with the highest average rating in Feb 2020.  

- First part:  
  - Count ratings per user using `GROUP BY user_id`.  
  - Order by rating count (desc) and username (asc) to break ties.  
  - Limit to top 1 user.  

- Second part:  
  - Filter ratings only in Feb 2020.  
  - Calculate average rating per movie.  
  - Order by average rating (desc), then movie title (asc).  
  - Limit to top 1 movie.  

- Combine both queries with `UNION ALL` to show the two results together in one column named `results`.  

### [1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT visited_on, amount_7d AS amount, average_amount
FROM (
    SELECT 
        visited_on,
        SUM(amount) OVER (
            ORDER BY visited_on
            ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
        ) AS amount_7d,
        ROUND(
            AVG(amount) OVER (
                ORDER BY visited_on
                ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
            ), 2
        ) AS average_amount,
        ROW_NUMBER() OVER (ORDER BY visited_on) AS row_num
    FROM (
        SELECT visited_on, SUM(amount) AS amount
        FROM Customer
        GROUP BY visited_on
    ) daily
) t
WHERE row_num >= 7
ORDER BY visited_on;
```
## Thought Process
- We need to calculate the **7-day rolling sum and average** of customer spending.  

- Step 1:  
  - First, aggregate the raw `Customer` table by `visited_on` to get daily totals.  

- Step 2:  
  - Use window functions:  
    - `SUM(amount) OVER (ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)` → gives the rolling 7-day total.  
    - `AVG(amount) OVER (ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)` → gives the rolling 7-day average.  
  - Round the average to 2 decimals.  

- Step 3:  
  - Assign row numbers ordered by `visited_on`.  
  - Exclude the first 6 rows (`WHERE row_num >= 7`) since a full 7-day window is required.  

- Step 4:  
  - Output columns: `visited_on`, total amount in 7 days, and average.  
  - Order by `visited_on` for chronological reporting.  
