[[Introduction To Relationships]]

## Designing One-to-One Relationships
To design a one-to-one relationship, you can either include all the columns from both tables in single table or create two separate tables and use a foreign key constraint to link them.
```
-- Option 1: Single table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    manager_first_name VARCHAR(50),
    manager_last_name VARCHAR(50)
);

-- Option 2: Two tables with foreign key
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    manager_id INT UNIQUE,
    FOREIGN KEY (manager_id) REFERENCES employees(employee_id)
);
```

## Designing One-to-Many Relationships
To design a one-to-many relationship, you typically create two tables: a parent table (the "one" side) and a child table (the "many" side). The child table includes a foreign key column that references the primary key of the parent table.
```
-- Parent table
CREATE TABLE teachers (
    teacher_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

-- Child table
CREATE TABLE classes (
    class_id INT PRIMARY KEY,
    class_name VARCHAR(100),
    teacher_id INT,
    FOREIGN KEY (teacher_id) REFERENCES teachers(teacher_id)
);
```

## Designing Many-to-Many Relationships
To design a mnay-to-many relationship, you typically crate a third table (called a junction table or associative table) that links the two main tables together. This junction includes a foreign key columns that reference the primary

```
-- Table 1
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

-- Table 2
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    description TEXT
);

-- Junction or Intemediary table
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```


## Parent Table and Child Tables
In a one-to-many or many-to-many relationship, the table on the "one" side is often referred to as the parent table, while the table on the "many" side is called the child table. The child table contains a foreign key that references the primary key of the parent table.

For example, in the teacher-class relationship, the *teachers* table is the parent table, and the *classes* table is the child table. Similarly, in the student-course relationship, the *students* and *courses* tables are parent tables.  