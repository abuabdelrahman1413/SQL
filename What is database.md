[[SQL]]
## Database and SQL: A Project-Based Learning Guide

This guide will equip you with the fundamental knowledge of databases and SQL, providing practical examples and project-oriented learning to solidify your understanding. We'll explore the concepts in a clear and concise manner, using real-world scenarios and visual aids. 

### 1.  What is a Database?

A database is an organized collection of data, typically stored electronically. Think of it as a digital filing system, but instead of physical folders, you have tables containing rows and columns.

**Example:** 
Imagine a library catalog. It has books organized by authors, titles, subjects, etc. A database mirrors this, storing information about each book (title, author, genre, etc.) in a structured way.

### 2. What is a Relational Database?

A relational database is a type of database where data is organized into tables with relationships between them. This relationship allows data to be connected and queried efficiently.

**Example:**
In the library example, you might have two tables: "Books" and "Authors." The "Books" table stores book details, while the "Authors" table stores author information. You could connect a book to its author by using a common identifier (author ID) in both tables.

### 3. What does SQL stand for?

SQL stands for **Structured Query Language**. It's a standardized language used to communicate with and manage relational databases. 

### 4. What is MySQL?

MySQL is a popular **Relational Database Management System (RDBMS)**. It's free, open-source, and widely used in various applications like web development, data analysis, and more.

### 5. How to Create a Database in MySQL?

To create a database in MySQL, you use the `CREATE DATABASE` command:

```sql
CREATE DATABASE my_database;
```

This will create a database named "my_database." 

### 6. What does DDL and DML stand for?

* **DDL (Data Definition Language):** This is used to define and modify the structure of your database. It includes commands like `CREATE`, `ALTER`, and `DROP`.
* **DML (Data Manipulation Language):** This is used to manipulate the data within your database. It includes commands like `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.

### 7. How to CREATE or ALTER a Table?

**CREATE TABLE:**

```sql
CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(255),
    author_id INT,
    genre VARCHAR(50)
);
```

**ALTER TABLE:**

```sql
ALTER TABLE Books
ADD COLUMN publication_year INT;
```

This adds a new column "publication_year" to the "Books" table.

### 8. How to SELECT Data from a Table?

```sql
SELECT * FROM Books;
```

This will display all columns and rows from the "Books" table.

**Filtering Data:**

```sql
SELECT title, author_id FROM Books WHERE genre = 'Fiction';
```

This will display the title and author ID of all books in the "Fiction" genre.

### 9. How to INSERT, UPDATE or DELETE Data?

**INSERT:**

```sql
INSERT INTO Books (book_id, title, author_id, genre) 
VALUES (1, 'The Lord of the Rings', 1, 'Fantasy');
```

**UPDATE:**

```sql
UPDATE Books
SET genre = 'Sci-Fi'
WHERE book_id = 2;
```

**DELETE:**

```sql
DELETE FROM Books WHERE book_id = 3;
```

### 10. What are Subqueries?

Subqueries are queries nested within other queries. They allow you to filter data based on the results of another query.

**Example:**

```sql
SELECT * FROM Books WHERE author_id IN (SELECT author_id FROM Authors WHERE city = 'New York');
```

This retrieves all books written by authors living in New York City.

### 11. How to Use MySQL Functions?

MySQL offers various built-in functions for data manipulation and calculations.

**Example:**

```sql
SELECT title, LENGTH(title) AS title_length FROM Books;
```

This calculates the length of each book title and displays it in a new column "title_length."

### 12. Backtick vs. Apostrophe

* **Backticks (`)**: Used to enclose identifiers (table names, column names) that might be reserved words or contain special characters.
* **Apostrophes (')**: Used to enclose literal string values.

**Example:**

```sql
SELECT * FROM `My Table`; -- Use backticks for table name
INSERT INTO Books (title) VALUES ('The Hitchhiker's Guide to the Galaxy'); -- Use apostrophes for string value
```

### 13.  MySQL Cheat Sheet & Resources:

* **MySQL Cheat Sheet:** [https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html) 
* **MySQL 8.0 SQL Statement Syntax:** [https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html)
* **Installing MySQL in Ubuntu 20.04:** [https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)


### Project-Based Learning:

Now, let's put these concepts into practice with a real-world project. 

**Scenario:** You are creating a database for a bookstore.

**1. Create the database:**

```sql
CREATE DATABASE bookstore;
```

**2. Create the "Books" table:**

```sql
CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(255),
    author_id INT,
    genre VARCHAR(50),
    price DECIMAL(5,2),
    publication_year INT
);
```

**3. Create the "Authors" table:**

```sql
CREATE TABLE Authors (
    author_id INT PRIMARY KEY,
    author_name VARCHAR(255),
    country VARCHAR(50)
);
```

**4. Insert some sample data:**

```sql
INSERT INTO Books (book_id, title, author_id, genre, price, publication_year) 
VALUES 
(1, 'The Lord of the Rings', 1, 'Fantasy', 19.99, 1954),
(2, '1984', 2, 'Dystopian', 10.99, 1949),
(3, 'Pride and Prejudice', 3, 'Romance', 9.99, 1813);

INSERT INTO Authors (author_id, author_name, country) 
VALUES 
(1, 'J.R.R. Tolkien', 'United Kingdom'),
(2, 'George Orwell', 'United Kingdom'),
(3, 'Jane Austen', 'United Kingdom');
```

**5. Write SQL queries to answer the following questions:**

* **List all books by a specific author:**
   ```sql
   SELECT title FROM Books WHERE author_id = 2;
   ```
* **Find the average price of books in a certain genre:**
   ```sql
   SELECT AVG(price) FROM Books WHERE genre = 'Fantasy';
   ```
* **List the books published after a specific year:**
   ```sql
   SELECT title FROM Books WHERE publication_year > 1980;
   ```
* **Find the author with the most books published:**
   ```sql
   SELECT author_name, COUNT(book_id) AS books_count 
   FROM Authors 
   JOIN Books ON Authors.author_id = Books.author_id
   GROUP BY author_name
   ORDER BY books_count DESC
   LIMIT 1;
   ```

**6. Expand the database by adding new tables like "Customers", "Orders", etc., and experiment with more complex queries to explore relationships between tables.**

**7. Use MySQL functions to perform calculations and manipulate data.**


### Problems:

**Here are 10 problems of increasing difficulty to test your knowledge:**

**1.** Find all books published before 2000.
**2.** List all authors who have written more than 3 books.
**3.** Find the average price of all books in each genre.
**4.** Retrieve the most expensive book published in each genre.
**5.** List all books that have the same title as the most expensive book in their genre.
**6.** Create a new table called `Genres` to store genre information, then update the `Books` table to reference genres from the `Genres` table.
**7.** Calculate the total revenue generated from each genre.
**8.** Find the books with the highest price difference compared to the average price of their genre.
**9.**  Update the price of all books by a certain author by a fixed percentage.
**10.** Write a query to create a new table that stores a summary of the most popular books based on the number of times they have been ordered.

**Solutions:**

The solutions to these problems will be provided in a separate document to ensure you practice your SQL skills before peeking at the answers.

**Remember:** 

*  Practice is key to mastering SQL. 
*  Don't be afraid to experiment and explore different approaches to solve problems.
*  The more you work with SQL, the more comfortable you will become with its syntax and capabilities.

By following this project-based learning guide and working through the problems, you will gain a strong understanding of databases and SQL, preparing you to work with data in various applications.