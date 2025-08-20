# Select Questions

This file has all the problems from the **Select** section of SQL50.  
Each question has a link, my SQL solution, and a short thought process written in bullet points for clarity.

---

### [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT product_id 
FROM Products 
WHERE low_fats = 'Y' AND recyclable = 'Y';
```
## Thought Process
- The table contains product details.
- We only want products that are **both** low fat and recyclable.
- That means two conditions should be true at the same time.
- I used the `WHERE` clause with:
    `low_fats = 'Y'`
    `recyclable = 'Y'`
- The `AND` ensures both conditions are satisfied together.
- Final output → product IDs that meet both conditions.

### [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50)

```sql
SELECT name 
FROM Customer 
WHERE referee_id != 2 OR referee_id IS NULL;
```
## Thought Process
- The table has customer details including who referred them (`referee_id`).
- We want all customers **except the ones referred by customer 2**, and also include customers who were **not referred by anyone**.
- Used `WHERE referee_id != 2` to exclude referrals from customer 2.
- Used `OR referee_id IS NULL` to include customers without any referee.
- Final output → names of all customers meeting these conditions.


