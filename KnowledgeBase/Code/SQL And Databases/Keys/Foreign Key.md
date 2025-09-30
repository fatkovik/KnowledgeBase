[[Introduction to Keys]]
A foreign Key is a column or a combination of columns in one table that references the primary key of another table. It establishes a link between the two tables and enforces referential integrity*, ensuring that data in the child table is calid and consistent with the data in the parent table.

**Referential Integrity** => *a database rule that ensures relationships between tables remain valid by requiring that any foreign key value must correspond to an existing, valid primary key value in the referenced table*

![[ForeignKeyExample.png]]

## NOT NULL Foreign Key

In some cases, it might be desirable to have a NOT NULL constraint on a foreign key column, meaning that the column cannot have a null value. This constraint ensures that every record in the child table is associated with a valid record in the parent table.

![[NonNullForeignKeyexample.png]]

## Foreign Key Constraints 

Foreign key constraints define the rules for referential integrity between tables. These constraints can include actions to be taken when a referenced record in the parent table is updated or deleted, such as:
- `CASCADE`: When a record in the parent table is updated or deleted, the corresponding records in the child table are also updated or deleted.
- `SET NULL`: When a record in the parent table is updated or deleted, the corresponding foreign key values in the child table are set to NULL.
- `NO ACTION`: When a record in the parent table is updated or deleted, the corresponding foreign key values in the child table remain unchanged, and the operation is rolled back if it violates referential integrity.

```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON UPDATE CASCADE ON DELETE SET NULL
);
```
