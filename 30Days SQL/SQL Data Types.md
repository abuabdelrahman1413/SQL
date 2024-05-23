[[SQL]]
# SQL Data Types

SQL data types define the type of data that can be stored in a column. Each column in a database table is required to have a name and a data type. The data type is a guideline for SQL to understand what type of data is expected inside each column, and it also identifies how SQL will interact with the stored data.

## Numeric Data Types

1. **INT**: A normal-sized integer that can be signed or unsigned.
    - Example: `INT`, `INTEGER`
    - ```sql
      CREATE TABLE ExampleTable (
          ID INT
      );
      ```

2. **SMALLINT**: A smaller integer.
    - Example: `SMALLINT`
    - ```sql
      CREATE TABLE ExampleTable (
          SmallNumber SMALLINT
      );
      ```

3. **DECIMAL**: A fixed-point number with a specified number of digits.
    - Example: `DECIMAL(p, s)` where `p` is the precision and `s` is the scale.
    - ```sql
      CREATE TABLE ExampleTable (
          Salary DECIMAL(10, 2)
      );
      ```

4. **FLOAT**: A floating-point number.
    - Example: `FLOAT`
    - ```sql
      CREATE TABLE ExampleTable (
          Temperature FLOAT
      );
      ```

## String Data Types

1. **CHAR**: A fixed-length string.
    - Example: `CHAR(n)` where `n` is the string length.
    - ```sql
      CREATE TABLE ExampleTable (
          Gender CHAR(1)
      );
      ```

2. **VARCHAR**: A variable-length string.
    - Example: `VARCHAR(n)` where `n` is the maximum string length.
    - ```sql
      CREATE TABLE ExampleTable (
          Name VARCHAR(50)
      );
      ```

3. **TEXT**: A large variable-length string.
    - Example: `TEXT`
    - ```sql
      CREATE TABLE ExampleTable (
          Description TEXT
      );
      ```

## Date and Time Data Types

1. **DATE**: A date value (year, month, day).
    - Example: `DATE`
    - ```sql
      CREATE TABLE ExampleTable (
          BirthDate DATE
      );
      ```

2. **TIME**: A time value (hour, minute, second).
    - Example: `TIME`
    - ```sql
      CREATE TABLE ExampleTable (
          AppointmentTime TIME
      );
      ```

3. **DATETIME**: A date and time value.
    - Example: `DATETIME`
    - ```sql
      CREATE TABLE ExampleTable (
          OrderDateTime DATETIME
      );
      ```

## Binary Data Types

1. **BINARY**: A fixed-length binary string.
    - Example: `BINARY(n)` where `n` is the length.
    - ```sql
      CREATE TABLE ExampleTable (
          BinaryData BINARY(16)
      );
      ```

2. **VARBINARY**: A variable-length binary string.
    - Example: `VARBINARY(n)` where `n` is the maximum length.
    - ```sql
      CREATE TABLE ExampleTable (
          VarBinaryData VARBINARY(256)
      );
      ```

## Other Data Types

1. **BOOLEAN**: Stores TRUE or FALSE values.
    - Example: `BOOLEAN`
    - ```sql
      CREATE TABLE ExampleTable (
          IsActive BOOLEAN
      );
      ```

2. **ENUM**: A string object that can have one value, chosen from a list of values.
    - Example: `ENUM('value1', 'value2', 'value3')`
    - ```sql
      CREATE TABLE ExampleTable (
          Status ENUM('Pending', 'Active', 'Inactive')
      );
      ```

3. **UUID**: A universally unique identifier.
    - Example: `UUID`
    - ```sql
      CREATE TABLE ExampleTable (
          UniqueID UUID
      );
      ```

## Example Table Using Various Data Types

```sql
CREATE TABLE SampleTable (
    ID INT PRIMARY KEY,
    Name VARCHAR(100),
    BirthDate DATE,
    Salary DECIMAL(10, 2),
    IsActive BOOLEAN,
    Description TEXT,
    UniqueID UUID,
    Status ENUM('Pending', 'Active', 'Inactive')
);
