[[Introduction To Database Normalization]]
The Second Normal Form (2NF) builds upon 1NF by addressing the issue of partial dependencies. A table is in 2NG if it is in 1NF and every non-prime attribute (column) is fully dependent on the entire primary key. ?tf

In other words, if a table has a composite primary key (consisting of multiple columns) then all non-key columns must depend on the entire primary key, not just part of it.

For example, consider a table with a composite primary key of *(studient_id, course_id)* and a columns *grade*. if *grade* column depends only on the *course_id* ad not on the combination of *student_id* and *course_id* then the table violates 2NF.

```
-- Violates 2NF
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    course_name VARCHAR(100), -- Depends only on course_id, not the entire primary key
    grade CHAR(2), 
    PRIMARY KEY (student_id, course_id)
);

-- Conforms to 2NF
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    grade CHAR(2),
    PRIMARY KEY (student_id, course_id)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);
```

