# SQL/Postgress Challenge

Suppose you have a database with three tables: "users", "orders", and "products". The "users" table contains columns id, name, and email. The "orders" table contains columns id, user_id, product_id, quantity, and created_at. The "products" table contains columns id, name, price, and category.

Write a single SQL query that returns a list of all users who have made at least 3 orders in the "Electronics" category and have spent more than $1000 on those orders, sorted by the total amount they have spent in descending order. The output should include the user's name, email, and the total amount they have spent on "Electronics" orders.

## Query

```sql
SELECT
  u.name,
  u.email,
  SUM(o.quantity * p.price) AS total_amount_spent
FROM
  users u
  JOIN orders o ON u.id = o.user_id
  JOIN products p ON o.product_id = p.id
WHERE
  p.category = 'Electronics'
GROUP BY
  u.id
HAVING
  COUNT(DISTINCT o.id) >= 3
  AND total_amount_spent > 1000
ORDER BY
  total_amount_spent DESC;
```

## Explanation

First, I combined the users with the orders they have and the products associated to those products. In a first approach, I made a LEFT JOIN clause to also return users withour orders, but seems much sense in using the JOIN clause since we only want users with more than three orders. I have asumme that every order has at least one product.


I startted combining the "users", "orders", and "products" tables using JOIN statements, so I can retrieve the combined data from all those tables. Instead of using a LEFT JOIN clause, I am using a JOIN clause because I only want to include users who have made orders. I assumed that that every order has at least one product, so using a JOIN clause is appropriate in this case.

Finally, I have filtered the results using a WHERE clause, specifying that only orders in the "Electronics" category should be included.

The query is finally grouping the results by the user's ID with the GROUP BY clause. This allow me to aggregate the order information for each user, so if I add the HAVING clause with the conditions COUNT(DISTINCT o.id) >= 3 and the total_amount_spent > 1000, I can retrieve the asked information.

Finally, we sort the output by the total amount spent in descending order using the ORDER BY clause.

The result of the query will include the user's name, email, and the total amount they have spent on "Electronics" orders.