# What is Object-Relational Mapping?

## Learning Goals

- Identify the impedance mismatch that exists between object-oriented and relational data models.
- Define the properties and benefits of Object-Relational Mapping (ORM) 

## Introduction

An impedance mismatch occurs when
data needs to be transformed into a different architectural paradigm.
Relational database models represent data in a tabular format, whereas object-oriented languages like
Java represent it as an interconnected graph of objects. There are many issues
that may arise when persisting objects to an RDBMS, including how to manage
object references, the concept of identity, object nesting, differences in scalar data types,
class inheritance, and many others.

**Object-Relational Mapping (ORM)** solves the impedance mismatch by defining
how an object and its properties
are related to one or more tables in the database. 
ORM uses the mapping information to manage the process of converting
data between object and table form.  ORM
generates the SQL to insert, update, and delete data
when the application changes object state, and facilitates
the querying of objects from the database.
This supports separate of concerns,
with the data management abstracted away from the application logic.

## Object-Oriented to RDBMS model mismatch

Java does not use a tabular data structure to store data like a relational database.
Instead, classes are used to model and store data. 

As we saw in the JDBC lessons, we can write code to explicitly map a Java class
to a relational database table.

For example, given the following `Employee` class: 

```java
public class Employee {
    private int id;
    private String email;
    private String office;
    private double salary;

    //constructor, getters, setters, etc
    
```

We define a database table to persist `Employee` objects as shown below.
Each attribute of the class is implemented as a table column:

```sql
CREATE TABLE employee (id INTEGER PRIMARY KEY, email TEXT, office TEXT, salary DECIMAL)"
```

An `Employee` class instance is saved to the database by setting the SQL `INSERT` statement
values to the object attributes:

```java
String insertStatement = String.format("INSERT INTO employee (id, email, office, salary) VALUES (%d, \'%s\', \'%s\', %.2f)",
                                 employee.getId(), employee.getEmail(), employee.getOffice(), employee.getSalary());
```

We can query the table and map the resulting row into an `Employee` class instance:

```java
ResultSet rs = statement.executeQuery("SELECT * FROM employee WHERE id = " + id;);
...
Employee employee = new Employee(rs.getInt("id"), rs.getString("email"), rs.getString("office"), rs.getDouble("salary"));
```

While this coding approach works, there are several issues that may arise:

- What if we need to modify the object model, for example adding new instance variables "jobTitle"
  and "startingDate"?  The relational model defined by the `CREATE TABLE` and `INSERT` statements would no longer
  match the object-oriented model, and must be explicitly maintained.
- What if we need to implement class inheritance, such as adding subclasses for exempt and non-exempt employees,
  full-time and part-time employees, etc?  An RDBMS is designed to model association relationships,
  not class inheritance relationships, and it is challenging to persist and query objects in the presences of inheritance hierarchies.
- Object-oriented languages represent association and composition relationships using object references,
  whereas an RDBMS represents relationships as a foreign key column. Data navigation and object traversal
  may differ between an RDBMS and an object-oriented program. 


## Object-Relational Mapping (ORM)

**Object-Relational Mapping (ORM)** is a mechanism designed to solve many of these issues.

- ORM makes it possible to persist, access and manipulate objects in an RDBMS without having to
  write explicit SQL code.
- ORM wraps implementation specific details of database storage drivers in an API.
- ORM provides methods to perform the most common database operations called CRUD (Create, Read, Update, Delete).
- ORM provides methods to specify queries based on classes and fields.

Once we have properly mapped a class to a table, its attributes to columns,
and defined relationships, we can use ORM 
methods to easily synchronize data between the program and the database.

## Conclusion

ORM solves the impedance mismatch between object-oriented and relational paradigms.
By making it easier to persist, access, and manipulate objects in a database, ORM
allows a programmer to focus on coding the application logic.