[[Introduction To Database Normalization]]
The First Normal Form (1NF) is the most basic form of normalization. It states that an attribute (Column) is a table must have atomic values, meaning each cell in the table should contain a single value, not a set of values.

For example, consider a table with a column named "PhoneNumbers" that store multiple phone numbers for a customer. This violates 1NF because the column contains a set of values instead of a single value. To conform to 1NF, you would need to separate the phone numbers into individual columns or create a separate table for phone numbers.

```
-- Violates 1NF
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    phone_numbers VARCHAR(200) -- Stores multiple phone numbers, violating 1NF
);

-- Conforms to 1NF
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    phone1 VARCHAR(20),
    phone2 VARCHAR(20),
    phone3 VARCHAR(20)
);
```