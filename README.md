# Database Operations

## Create Database

```sql
CREATE DATABASE [IF NOT EXISTS] database_name;
```

## Check and Display Databases

```sql
SHOW DATABASES;
```

## Select Database to Work With

```sql
USE database_name;
```

## Show Tables in Database

```sql
SHOW TABLES;
```

## Delete Database

```sql
DROP DATABASE [IF EXISTS] database_name;
```

# Data Types

## Numeric Types

- `TINYINT` (BOOLEAN) - 1 byte
- `SMALLINT` - 2 bytes
- `MEDIUMINT` - 3 bytes
- `INT/INTEGER` - 4 bytes
- `BIGINT` - 8 bytes
- `FLOAT` - 4 bytes
- `DOUBLE` - 8 bytes
- `DECIMAL` - depends on definition

## String Types

- `CHAR` - Fixed-length character string
- `VARCHAR` - Variable-length character string
- `BINARY` - Fixed-length binary string
- `VARBINARY` - Variable-length binary string
- `TINYBLOB` - Very small binary object
- `BLOB` - Small binary object
- `MEDIUMBLOB` - Medium-sized binary object
- `LONGBLOB` - Large binary object
- `TINYTEXT` - Very small text string
- `TEXT` - Small text string
- `MEDIUMTEXT` - Medium-sized text string
- `LONGTEXT` - Large text string

## Date and Time Types

- `DATE` - 'YYYY-MM-DD', 3 bytes, accuracy: 1 day
- `TIME` - 'hh:mm:ss', 3-5 bytes, accuracy: 100 nanoseconds
- `DATETIME` - 'YYYY-MM-DD hh:mm:ss', 8 bytes, accuracy: 0.00333 seconds
- `TIMESTAMP` - 'YYYY-MM-DD hh:mm:ss'
- `YEAR` - 'YYYY', range: '1901' to '2155', and '0000'

# Create Table

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
  column_name data_type [default_value] [column_constraints],
  ...
  table_constraints
) ENGINE=table_type;
```

- `default_value`: Default value for a column if not specified (default is NULL)
- `table_type`: Storage engine type (default is InnoDB for MySQL 5.5)
- `constraints`: Primary Key, Foreign Key, Not Null, Unique, Check
- `column_constraints`: Applied to a specific column
- `table_constraints`: Applied to one or more columns

## Constraints

- `PRIMARY KEY`: Uniquely identifies each row in a table
- `NOT NULL`: Ensures a column cannot have NULL value
- `UNIQUE`: Ensures all values in a column are unique (can be NULL if NOT NULL is not applied)
- `CHECK`: Not supported by MySQL, can be declared but has no effect

## Primary Key Constraints

### Column Level

```sql
column_name data_type [CONSTRAINT constraint_name] PRIMARY KEY
```

### Table Level

```sql
[CONSTRAINT constraint_name] PRIMARY KEY (column_name1, column_name2, ...)
```

## Naming Constraints

```sql
CONSTRAINT constraint_name constraint_definition
```

- Useful for error handling when constraint violations occur

## Foreign Key Constraints

```sql
CONSTRAINT fk_name FOREIGN KEY (column_name) REFERENCES parent_table (parent_column) [ON DELETE RESTRICT] [ON UPDATE CASCADE]
```

- `ON DELETE RESTRICT`: Prevents deletion of referenced data
- `ON UPDATE CASCADE`: Automatically updates referencing data

# Alter Table

```sql
ALTER TABLE table_name [option]
  ADD [COLUMN] column_definition,
  MODIFY [COLUMN] column_definition,
  DROP [COLUMN] column_name,
  ADD table_constraint,
  DROP constraint_name;
```

# Select Statement

```sql
SELECT column1, column2, ... (* for all)
FROM table_name
[WHERE condition]
[GROUP BY column]
[HAVING condition]
[ORDER BY column]
[LIMIT number];
```

- `WHERE`: Filters rows based on condition
  - `AND/OR`: Combines conditions
  - `IS NULL`: Finds NULL values
- `LIMIT`: Limits the number of returned records

## LIMIT Clause

### First N Records

```sql
SELECT * FROM table_name
LIMIT N;
```

### N Records Starting from S

```sql
SELECT * FROM table_name
LIMIT S, N;
```

## DISTINCT Keyword

Removes duplicate data from SELECT statement.

```sql
SELECT DISTINCT column_name FROM table_name;
```

- Example:

```sql
SELECT DISTINCT jobTitle FROM Employees;
```

```

```
