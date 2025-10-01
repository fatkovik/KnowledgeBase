[[Data Structures in DB core]]

In the world of databases, data types are like different shapes of containers that hold specific types of information. Just as you wouldn't store liquids in a basket or solid objects in a jar, databases need to enforce specific data types to ensure data integrity and consistency.

Some common data types in SQL include:

- `INT` or `INTEGER`: Stores whole numbers, like `42` or `17`.
- `FLOAT` or `DOUBLE`: Stores decimal numbers, like `3.14159` or `0.00005`.
- `VARCHAR` or `TEXT`: Stores text data, like names or descriptions.
- `DATE` or `DATETIME`: Stores date and time values, like `'2023-05-06'` or `'2024-01-01 12:34:56'`.
- `BOOLEAN`: Stores true/false values, like `1` (true) or `0` (false).

Choosing the right data type is crucial because it affects how the data is stored, queried, and manipulated. For example, trying to store a large string in an `INT` column would result in an error or data truncation.  

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT,
    is_active BOOLEAN DEFAULT 1
);
```
*In this example, we create a `users` table with columns for `id` (integer), `name` (string of up to 50 characters), `age` (integer), and `is_active` (boolean, with a default value of `1` or true).*