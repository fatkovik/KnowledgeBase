[[Introduction To Database Normalization]]

The Third Normal Form (3NF) builds upon 2NF by addressing the issue of transitive dependencies. A table is in 3NF if it is in 2NF and every ***non-prime*** attribute is non-transitively dependent on the primary key.

In other words, if a non-key columns is dependent on another non-key column, then the table violates 3NFm and the non-key columns should be separated into their own table.

For example, consider a table with columns `student_id` `student_name`, `class_id`, and `class_name`. The `student_name` column depends on the `student_id`, and the `class_name` column depends on the `class_id`. However, the `class_name` column also transitively depends on the `student_id` through the `class_id` column. This violates 3NF.

```
-- Violates 3NF
CREATE TABLE student_classes (
    student_id INT,
    student_name VARCHAR(100),
    class_id INT,
    class_name VARCHAR(100),
    PRIMARY KEY (student_id, class_id)
);

-- Conforms to 3NF
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100)
);

CREATE TABLE classes (
    class_id INT PRIMARY KEY,
    class_name VARCHAR(100)
);

CREATE TABLE student_classes (
    student_id INT,
    class_id INT,
    PRIMARY KEY (student_id, class_id),
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (class_id) REFERENCES classes(class_id)
);
```