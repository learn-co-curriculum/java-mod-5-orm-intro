# What is Object-Relational Mapping?

## Learning Goals

- Explain the concept of an ORM and why we build them.

## Introduction

Programming languages and relational databases handle data differently.
Object-relational mapping (ORM) helps solve this issue by mapping database data
into a format used by a programming language and vice versa. The main parts of
an ORM are tables (virtual), relationships, and object methods.

## Mapping Classes into Tables

Programming languages don’t have tables to store data like relational databases.
Instead, classes are used as table descriptions. We use a class to define the
database table structure and add methods to interact with the data.

The data in each row of the database table can be used to create new instances
of a class. The instance can manipulate both the data in the table and its
relationships.

As an example, look at the following `USER` class and table. Each attribute of
the class is directly mapped to the table column. For more complex data in the
programming language such as lists or enums, we have to use special methods or
techniques to map them. We will take a look at these later.

![ORM to table mapping](https://curriculum-content.s3.amazonaws.com/java-spring-1/orm-table-example.png)

## Relationships

When you delete a reference to an object in a programming language from a second
object it doesn’t remove references from any other objects. But in relational
databases, when a row is deleted it causes cascade deletions of all related data
in other tables.

![Untitled](https://curriculum-content.s3.amazonaws.com/java-spring-1/user-comments.png)

For example, If we delete a user row in a relational database that references
comments made by the user in the Comment table, the comments will also be
deleted along with the user. In this case, the comments belong to the user so
without the associated user, the comments don’t make sense as a separate entity.
However, deleting a comment won’t delete user data from the database.

When we use an ORM, we have to explicitly define relationships across classes to
ensure that working with object instances in a programming language maintains
and updates relationships properly.

## Object Methods

An ORM provides methods to perform the most common database operations called
CRUD (Create, Read, Update, Delete). Once we have properly mapped a class to a
table, its attributes to columns, and defined relationships, we can use the
methods provided by the ORM to easily synchronize data between the program and
the database.

## Conclusion

An ORM makes it possible to map programming language classes to databases which
makes it easier to add database functionality to a program.
