[[DataBases]]

Joins are like bridges that connect different tables in a database, allowing you to combine and retrieve related data from multiple sources. They are a fundamental concept in relational databases and are essential for querying and manipulating data efficiently.

![[JoinCheatSheet.png]]

# **General Information 

## Alias

Aliases are like nicknames for tables or columns in SQL queries. They can make queries more readable and easier to understand, especially when dealing with long table or column names, or when referencing the same table multiple times in a query.  

```
SELECT u.name, o.order_date, p.product_name
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN products p ON o.product_id = p.id;

```

In this example, we use the aliases `u` for the `users` table, `o` for the `orders` table, and `p` for the `products` table. This makes the query more concise and easier to read, without having to repeat the full table names multiple times.

## JOIN with NOT NULL Columns

Sometimes, you may want to perform a join only on columns that are not null. This can be useful when you want to exclude rows with missing data from the result set.  

```
SELECT users.name, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id AND users.name IS NOT NULL;

```

In this example, we perform an inner join between the `users` and `orders` tables, but we add an additional condition `users.name IS NOT NULL` to ensure that only rows with non-null `name` values are included in the result set.