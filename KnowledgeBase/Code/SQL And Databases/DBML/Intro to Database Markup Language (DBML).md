[[DataBases]]

Database Modeling Language (DBML) is a simple and intuitive markup language for describing the structure of relation databases. It provides a human-readable way to define tables, columns, relationships, and constraints, making it easy to communicate and collaborate on database designs.


## **Getting Started with DBML**

To get started with DBML, you'll need a text editor and a basic understanding of database concepts. Let's create our first DBML file:  

```
// my_database.dbml

Table users {
  id int [pk, increment]
  username varchar
  email varchar [unique]
  created_at datetime [default: `now()`]
}

```

In this example, we've defined a `users` table with columns for `id`, `username`, `email`, and `created_at`. The `[pk]` tag specifies that `id` is the primary key, `[increment]` indicates auto-incrementing, `[unique]` ensures uniqueness for the `email`, and `[default:` now()`]` sets the default value of `created_at` to the current timestamp.


## **Creating Tables**

DBML allows you to define multiple tables and their columns in a single file. Let's add more tables to our database:  

```
// my_database.dbml

Table users {
  id int [pk, increment]
  username varchar
  email varchar [unique]
  created_at datetime [default: `now()`]
}

Table posts {
  id int [pk, increment]
  title varchar
  content text
  user_id int [ref: > users.id]
  created_at datetime [default: `now()`]
}

```

In this example, we've added a `posts` table with columns for `id`, `title`, `content`, `user_id`, and `created_at`. The `[ref: > users.id]` tag establishes a foreign key relationship between the `user_id` column in the `posts` table and the `id` column in the `users` table.


## **Defining Relationships**

DBML supports various types of relationships between tables, including one-to-one, one-to-many, and many-to-many. Let's define some relationships in our database:  

```
// my_database.dbml

Table users {
  id int [pk, increment]
  username varchar
  email varchar [unique]
  created_at datetime [default: `now()`]
}

Table posts {
  id int [pk, increment]
  title varchar
  content text
  user_id int [ref: > users.id]
  created_at datetime [default: `now()`]
}

Ref: users.id < posts.user_id

```

In this example, we've defined a one-to-many relationship between the `users` and `posts` tables. The `Ref: users.id < posts.user_id` line specifies that the `id` column in the `users` table is referenced by the `user_id` column in the `posts` table.


## **Adding Constraints**

Constraints ensure data integrity and enforce rules on the database. DBML supports various constraints such as primary keys, foreign keys, unique constraints, and default values. Let's add some constraints to our tables:  

```
// my_database.dbml

Table users {
  id int [pk, increment]
  username varchar [unique]
  email varchar [unique]
  created_at datetime [default: `now()`]
}

Table posts {
  id int [pk, increment]
  title varchar
  content text
  user_id int [ref: > users.id]
  created_at datetime [default: `now()`]
}

Ref: users.id < posts.user_id

```

In this updated example, we've added a `[unique]` constraint to the `username` column in the `users` table to ensure that each username is unique.

## **Documenting Your Database**

DBML allows you to add comments and annotations to your database schema, making it easier to understand and maintain. Let's document our tables with comments:  

```
// my_database.dbml

Table users {
  id int [pk, increment] // Unique identifier for users
  username varchar [unique] // User's username
  email varchar [unique] // User's email address
  created_at datetime [default: `now()`] // Date and time when the user was created
}

Table posts {
  id int [pk, increment] // Unique identifier for posts
  title varchar // Title of the post
  content text // Content of the post
  user_id int [ref: > users.id] // ID of the user who created the post
  created_at datetime [default: `now()`] // Date and time when the post was created
}

Ref: users.id < posts.user_id // Relationship between users and posts

```
