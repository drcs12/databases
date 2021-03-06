% SQL Data Definition
% CS 4400

# Sturctured Query Language

- Practical implementation of the relational model
- Originally SEQUEL (Structured English QEUry Language) at IBM research
- SQL became standard in 1986
- Supported by all major RDBMS vendors, with minor (and sometimes major) differences

SQL's big advantage: if you stick to ANSI SQL, your database code is portable between RDBMS systems.

# SQL Relational Model

- Relations are *tables*
- Tuples are *rows*
- Attributes are *columns*

For the most part these terms are interchangeable.

- Important difference: tables allow duplicate rows

# Schemas and Catalogs

A *schema* (database in the relational model) is a collection of related tables and constructs. A schema has:

- a schema name
- an authorization identifier (user who owns the schema)

In MySQL `create schema` is a synonym for `create database`.

A catalog is a named collection of schemas. MySQL includes a `table_catalog` column in its `information_schema.tables` table for compatibility with the SQL standard, but does not use catalogs.

# CREATE TABLE

The `CREATE TABLE` command creates a *base table* (`CREATE VIEW` creates a *virtual* or *derived* table):

General form:
```sql
CREATE TABLE <table_name> (
 <column_name> <column_type> <column_constraints>...,
 [... ,]
 <table_constraints>,
 [...]
);
```

# CREATE TABLE Example

```sql
CREATE TABLE pub (
  pub_id INT PRIMARY KEY,
  title VARCHAR(16) NOT NULL,
  book_id INT NOT NULL REFERENCES book(book_id)
);
```

By convention, SQL keywords are in ALL CAPS in instructional examples but not when typing.

Note: see [pubs-schema.sql](http://www.cc.gatech.edu/~simpkins/teaching/gatech/cs4400/resources/pubs-schema.sql) and [pubs-data.sql](http://www.cc.gatech.edu/~simpkins/teaching/gatech/cs4400/resources/pubs-dta.sql) for examples of SQL database creation and population commands.

# Attribute Types

- Numeric data types
    - Integer numbers: INTEGER, INT, and SMALLINT
    - Floating-point (real) numbers: FLOAT or REAL, and DOUBLE PRECISION
- Character-string data types
    - Fixed length: CHAR(n), CHARACTER(n)
    - Varying length: VARCHAR(n), CHAR VARYING(n), CHARACTER VARYING(n)

# Bits and Booleans

- Bit-string data types
    - Fixed length: BIT(n)
    - Varying length: BIT VARYING(n)
- Boolean data type
    - Values of TRUE or FALSE or NULL
- Dates and Timestamps
    - YEAR, MONTH, and DAY in the form YYYY-MM-DD
    - Multiple mapping functions available in RDBMSs to change date formats

# Constraints

- Attribute (a.k.a. column) constraints
- Key (a.k.a. unique)
- Primary key
- Foreign key

We'll also learn named constraints, assertions and triggers when in Advanced SQL.

# Key and Primary Key Constraints

Key:

```sql
  name CHAR(10) UNIQUE,
```


Primary key:
```sql
  pub_id INT PRIMARY KEY,
```

A primary key is implicitly `UNIQUE`

# Foreign Key Constratins

```sql
  book_id INT NOT NULL REFERENCES book(book_id)
```

Notice also that we don't allow `book_id` to be `NULL`. So `pub` totally participates in its relationship with `book`.


# CHECK Constraints

```sql
CREATE TABLE bartender (
  id INT PRIMARY KEY,
  name VARCHAR(10) NOT NULL,
  age INT CHECK (age > 20)
);
```

Note: MySQL does not enforce `CHECK` constraints. We'll learn about triggers in Advanced SQL.
