[[Introduction to Joins]]

While inner joins are like friendly handshakes, outer joins are more like welcoming hugs. They include not only the matching rows from both tables but also the non-matching rows from one or both tables, depending on the type of outer join.

## Right Outer Join

A right outer join is like a warm hug from the right table to the left table. It includes all rows from the right table, along with the matching rows from the left table. If there are no matching rows in the left table, the result will contain `NULL` values for the left table's columns.  

```
SELECT users.name, orders.order_date
FROM users
RIGHT OUTER JOIN orders ON users.id = orders.user_id;
```

In this example, we retrieve all rows from the `orders` table (the right table), along with the matching `name` values from the `users` table (the left table). If an order doesn't have a matching user, the `name` column will contain `NULL`.

## JOIN with NOT NULL Columns

Sometimes, you may want to perform a join only on columns that are not null. This can be useful when you want to exclude rows with missing data from the result set.  

```
SELECT users.name, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id AND users.name IS NOT NULL;

```

In this example, we perform an inner join between the `users` and `orders` tables, but we add an additional condition `users.name IS NOT NULL` to ensure that only rows with non-null `name`values are included in the result set.

## Outer Join Across 3 Tables

Similar to the inner join example, we can perform outer joins across multiple tables. Let's say we want to retrieve all orders, along with the user's name and the product name, even if there are missing values in the `users` or `products` tables.  

```
SELECT users.name, orders.order_date, products.product_name
FROM orders
LEFT OUTER JOIN users ON orders.user_id = users.id
LEFT OUTER JOIN products ON orders.product_id = products.id;

```

Here, we start with the `orders` table and perform a left outer join with both the `users` and `products` tables. This ensures that all orders are included in the result set, along with the matching user names and product names if available. If there are no matching rows in the `users` or `products` tables, the respective columns will contain `NULL` values.