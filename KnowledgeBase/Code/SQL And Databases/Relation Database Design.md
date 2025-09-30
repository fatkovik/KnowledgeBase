[[SQL Fundametals]]

## What is a Relational Database?

A relational database is a type of database that organizes data into tables (relations) with rows (records) and columns (fields). These tables are interconnected through relationships, allowing data to be accessed and combined in various ways. Imagine a collection of spreadsheets, each representing a different aspect of your data, but with the ability to link and combine information across them seamlessly.

## What is Database Design?

Database design is the process of creating an efficient and organized structure for storing and managing data in a database.

Schema
![[DBSchema.png]]


## Data Integrity

Data integrity refers to the accuracy, consistency, and reliability of data stored in a database. It ensures that the data follows specific rules and constraints, preventing errors and inconsistencies. There are three types of data integrity:

1. **Entity Integrity**: Ensures each row in a table is uniquely identifiable by a primary key, and the primary key cannot have null values.
2. **Referential Integrity**: Maintains relationships between tables by ensuring foreign key values in one table match the primary key values in another table.
3. **Domain Integrity**: Enforces valid entries for a given column by restricting the data type, format, and range of values that can be stored.

Example code to enforce Data Integrity 
```
-- Example: Enforcing data integrity
CREATE TABLE orders (
    order_id INT PRIMARY KEY, -- Entity integrity
    customer_id INT FOREIGN KEY REFERENCES customers(customer_id), -- Referential integrity
    order_date DATE NOT NULL, -- Domain integrity
    total_amount DECIMAL(10, 2) CHECK (total_amount >= 0) -- Domain integrity
);
```

## Atomic Values

In database design, it's important to store atomic values, which means storing the smallest pieces of information that cannot be further divided. This principle helps maintain data integrity and avoid redundancy.

For example, instead of storing a customer's full name in a single column, it's better to separate it into first name and last name columns. This way, you can easily search, sort, or manipulate each part of the name independently.

