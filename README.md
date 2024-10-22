Tạo Database:

````markdown
# Database Operations

## Create Database

```sql
CREATE DATABASE [IF NOT EXISTS] database_name;
```
````

Check newly created DB / Show all DBs on the server:

```sql
SHOW DATABASES;
```

Select a DB to work with:

```sql
USE database_name;
```

Show tables in the DB:

```sql
SHOW TABLES;
```

Delete a Database (physically):

```sql
DROP DATABASE [IF EXISTS] database_name;
```

## Data Types

### Numeric

- `TINYINT(BOOLEAN)` - 1 byte
- `SMALLINT` - 2 bytes
- `MEDIUMINT` - 3 bytes
- `INT/INTEGER` - 4 bytes
- `BIGINT` - 8 bytes
- `FLOAT` - 4 bytes
- `DOUBLE` - 8 bytes
- `DECIMAL` - depends on definition

### String

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

### Time

- `DATE` - 'YYYY-MM-DD', 3 bytes, accuracy: 1 day
- `TIME` - 'hh:mm:ss', 3-5 bytes, accuracy: 100 nanoseconds
- `DATETIME` - 'YYYY-MM-DD hh:mm:ss', 8 bytes, accuracy: 0.00333 seconds
- `TIMESTAMP` - 'YYYY-MM-DD hh:mm:ss'
- `YEAR` - 'YYYY', range: '1901' to '2155', and '0000'

## Create Table

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
    column_name data_type [default_value] [column_constraints],
    ...
    table_constraints
) ENGINE=table_type;
```

- `default_value`: Default value for a column (default is NULL)
- `table_type`: Storage engine type (default is InnoDB in MySQL 5.5)
- `constraints`: Primary Key, Foreign Key, Not Null, Unique, Check
- `column_constraint`: Applied to a specific column
- `table_constraint`: Applied to one or more columns

### Constraints

- `PRIMARY KEY`: Uniquely identifies each row in the table
- `NOT NULL`: Ensures column value cannot be NULL
- `UNIQUE`: Ensures all values in a column are unique (can be NULL if NOT NULL is not applied)
- `CHECK`: Not supported in MySQL (declaration has no effect)

### Primary Key Constraints

- Column level:
  - `ON UPDATE CASCADE`: Automatically updates dependent records when referenced data changes
  - Default behavior for DELETE and UPDATE is RESTRICT if options are not specified

## Alter Table

```sql
ALTER TABLE table_name [option]
    ADD [COLUMN] column_definition,
    MODIFY [COLUMN] create_definition,
    DROP [COLUMN] column_name,
    ADD table_constraint,
    DROP constraint_name;
```

````
  ```sql
  column_name data_type [CONSTRAINT constraint_name] PRIMARY KEY
````

- Table level:
  ```sql
  [CONSTRAINT constraint_name] PRIMARY KEY (column_name1, column_name2, ...)
  ```

### Naming Constraints

- `CONSTRAINT <name> <constraint>`: Useful for error handling when constraint violations occur

### Foreign Key (Table level)

- Example: city -> country
  ```sql
  CONSTRAINT fk_city_country FOREIGN KEY (country_id)
  REFERENCES country (country_id) [ON DELETE RESTRICT] [ON UPDATE CASCADE]
  ```
  - `ON DELETE RESTRICT`: Prevents deletion of referenced data if there are dependent records
