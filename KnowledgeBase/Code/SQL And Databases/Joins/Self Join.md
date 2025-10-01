[[Introduction to Joins]]

## Self Join

A self join is like a table having a conversation with itself. It's a way to join a table with itself, based on a specific condition or relationship within the same table. This can be useful when dealing with hierarchical or recursive data structures, such as employee-manager relationships or nested categories.  

```
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT OUTER JOIN employees m ON e.manager_id = m.id;
```

In this example, we perform a self join on the `employees` table to retrieve the name of each employee and their corresponding manager's name. We use a left outer join to ensure that all employees are included in the result set, even if they don't have a manager assigned.