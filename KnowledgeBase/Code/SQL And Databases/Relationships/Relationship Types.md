[[Introduction To Relationships]]
There are 3 main types of relationships, which are:
## One-to-One Relationships
In a one-to-one relationship, each record in one table is associated with exactly one record in another table, and vice versa.

**For example**, consider a database where each employee has one and only one manager, and each manager manages one and only one employee. This type of relationship is relatively rare in practice.

![[OneToOneRelExample.png]]

## One-to-Many Relationships

In a one-to-many relationship, each record in one table (the "one" side) can be associated with multiple records in another table (the "many" side). 
**For example**, in a database for a school, one teach multiple classes, but each class is taught by only one teacher.
![[OneToManyRelTypeEaxmple.png]]

## Many-to-Many Relationships

In a many-to-many relationship, each record in one table can be associated with multiple records in another table, and vice versa.
**For example**, in a database for a university, a student can enroll in multiple courses, and each course can have multiple student enrolled.
![[ManyToManyRelExample.png]]