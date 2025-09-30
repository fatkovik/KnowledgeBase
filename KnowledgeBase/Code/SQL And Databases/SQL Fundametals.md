[[DataBases]]
### Structured Query Language

Allows us to retrieve insert update delete data from DB

Database Management System - *DBMS*
Basically a software that enables user to interact with databases
An interface to define, create and manage databases

specific type of it is Relation Database
organizes data into table with **rows** and **columns** Where:

Table -> Entity
Row -> Record (or an instance of that entity)
Column -> Attribute (or a property of that entity)

Here we define **CRUD**
Basic operation defined by this all shit

C -> Create is used to insert new record into a table
R -> Read is used to retrieve data from a table
U -> update is used to modify existing records
D -> is used to remove records from a table

***SQL Queries***
commands or instruction to a database basic ones are;

SELECT -> used to retrieve data from database allows us to specify columns and condition for filtering using WHERE clause

INSERT -> Add new record
UPDATE -> Modify existing record in the table
DELETE -> Used to delete a record
JOIN -> Combine rows from two or more tables based on a related column between them. Multiple types of JOIN exists s.t. INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN.

### Btw all the LINQ queries that we all use in C# are SQL queries aswell ###

Transaction -> sequence of one or more SQL operation treated as a Single unit, used for ensuring data integrity, and work in principle of ALL succeed or ALL fail.

There exists Stored procedures, basically precomplied SQL code that is stored and can be executed on SQL server,
Works with Triggers, a database objects that automatically execute in response to specific events 


***Below Cheatsheet for DB Terms***
## Database Terms

- **Table**: A collection of related data organized in rows and columns.
- **Row**: A single instance or entry in a table (also known as a record or tuple).
- **Column**: A specific characteristic or property of the data in a table (also known as a field or attribute).
- **Primary Key**: A column or combination of columns that uniquely identifies each row in a table.
- **Foreign Key**: A column or combination of columns that references the primary key of another table, establishing a relationship between the two tables.
- **Join**: An operation that combines rows from two or more tables based on a related column.
- **Index**: A data structure that improves the performance of data retrieval operations by creating a sorted representation of the data in a table.
- **View**: A virtual table that is dynamically generated from one or more underlying tables.
- **Stored Procedure**: A pre-compiled collection of SQL statements that can be executed as a single unit.
- **Trigger**: A special type of stored procedure that is automatically executed when a specific event occurs in a table, such as an INSERT, UPDATE, or DELETE statement.