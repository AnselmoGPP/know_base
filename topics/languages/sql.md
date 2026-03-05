# SQL


## Table of Contents

+ [**References**](#references)
+ [**SQL basics**](#sql-basics)
+ [**Manipulation**](#manipulation)
  + [Creating](#creating)
  + [Calling](#calling)
  + [Modifying](#modifying)
+ [**Queries**](#queries)
  + [AS, DISTINCT, WHERE, IS (NOT) NULL](#as-distinct-where-is-not-null)
  + [LIKE](#like)
  + [BETWEEN, AND, OR](#between-and-or)
  + [ORDER BY, LIMIT, DESC/ASC](#order-by-limit-desc-asc)
  + [CASE, THEN, ELSE, END](#case-then-else-end)
+ [**Aggregate functions**](#aggregate-functions)
  + [COUNT(), SUM(), MAX/MIN()](#count-sum-max-min)
  + [AVG(), ROUND()](#avg-round)
  + [GROUP BY](#group-by)
  + [HAVING](#having)
+ [**Multiple tables**](#multiple-tables)
  + [JOIN, ON](#join-on)
  + [LEFT JOIN](#left-join)
  + [CROSS JOIN](#cross-join)
  + [UNION](#union)
  + [WITH](#with)
+ [**Glossary**](#glossary)


## References

- [CodeAcademy](https://www.codecademy.com/search?query=SQL)
- [SQLite with C++](https://www.geeksforgeeks.org/database-connectivity-using-cc/)
- [SQLite Vs PostgreSQL](https://tableplus.com/blog/2018/08/sqlite-vs-postgresql-which-database-to-use-and-why.html)
- [GitHub repo](https://github.com/AnselmoGPP/SQL_tests)


## SQL basics

**SQL**:

- **SQL** (Structured Query Language): Programming language designed to manipulate and manage data stored in relational databases.
- **SQLite**: The most used SQL database engine in the world. Here, we use SQLite Relational Database Management System (RDMS).

**Database**:

- **Relational database**: Organizes information into one or more tables.
- **Table** (or Relation): Collection of data organized into rows and columns.
- **Column**: Set of data values of a particular type (integer, real, text, date [YYYY-MM-DD]).
- **Row**: Single record in a table.

**Components**:

- **Statement**: Text that the database recognizes as a valid command. They always end with semicolon (;). Elements:
  - **Clause** (or Command): Performs a specific task in SQL. In capital letters by convention.
  - **Table name**
  - **Parameter**: List of columns and data types or values that are passed to a clause as an argument.
- **NULL**: Special value that represents missing or unknown data. It cannot be tested with comparison operators (!=, >= …), only IS NULL and IS NOT NULL.
- **Querying**: Retrieving information stored in a database by asking questions and returning a result set with data relevant to the question.
- **Aggregates**: Calculations performed on multiple rows of a table.


## Manipulation

### Creating

Create a new table called `workers` with the columns `id` (integer), `name` (text) and `age` (integer):

```
CREATE TABLE workers (
    id INTEGER,
    name TEXT,
    age INTEGER );
```

**Constraints**: Say how a column can be used. A database can reject data that don’t adhere to certain restrictions.

- `PRIMARY KEY`: No row can have same value in this column. Only one possible column of this type.
- `UNIQUE`: No row can have same value in this column. Many possible `UNIQUE` columns.
- `NOT NULL`: Must have a value.
- `DEFAULT “abc”`: If an inserted row has no value specified, then it will be `abc`.

```
CREATE TABLE dishes (
    id INTEGER PRIMARY KEY,
    code INTEGER UNIQUE,
    condiments TEXT NOT NULL,
    name TEXT DEFAULT "soup" );
```

### Calling

Call table `people`:

```
SELECT * FROM people;
```

Call `age` column from table `people`:

```
SELECT age FROM people;
```

Call columns `age` and `name` from table `people`:

```
SELECT age, name FROM people;
```

### Modifying

Add a row to table `workers`:

```
INSERT INTO workers VALUES (1, 'John Smith', 25);
```

```
INSERT INTO workers (id, name, age)
VALUES (1, 'John Smith', 25);
```

Edit one row:

```
UPDATE workers
SET age = 23
WHERE id = 1;
```

Add a column (its values will be `NULL`):

```
ALTER TABLE workers
ADD COLUMN address TEXT;
```

Delete rows where `address` is `NULL` (and when is not `NULL`):

```
DELETE FROM workers
WHERE address IS NULL;     // IS NOT NULL
```


## Queries

### AS, DISTINCT, WHERE, IS (NOT) NULL

Rename a column (or table) using an alias (the alias only appears in the result, the columns have not been renamed in the table). Here, we rename `name` as `Titles`:

```
SELECT name AS 'Titles' FROM movies;
```

Call the unique values from column `genre`.

```
SELECT DISTINCT genre FROM movies;
```

Call the records where the values of column `rating` are > 8:

```
SELECT * FROM movies WHERE rating > 8;
```
- Some possible operators: `=`, `!=`, `<`, `>`, `<=`, `>=`

Call records where “rating” is not null (or those where is null).

```
SELECT * FROM movies WHERE rating IS NOT NULL;     // IS NULL;
```

### LIKE

`LIKE` is not case sensitive.

Call records where the value of `name` begins with `Se`, ends with `en`, and has one letter in the middle:

```
SELECT * FROM movies WHERE name LIKE 'To_as';
```

Names that begin with `To`:

```
... LIKE 'Jo%';
```

Names that end with `as`:

```
... LIKE '%as';
```

Names that contain the word ‘oma’:

```
... LIKE '%oma%';
```

### BETWEEN, AND, OR

`BETWEEN` supports numbers, text or dates.

- `BETWEEN` 2 letters, it doesn’t include the 2nd letter.
- `BETWEEN` 2 numbers, it includes de 2nd number.

Call records where `name` begins with D, E or F:

```
SELECT * FROM movies WHERE name BETWEEN 'D' AND 'G';
```

Call records where “year” is between 1980 and 1999, inclusive:

```
... BETWEEN 1980 AND 1999;
```

Multiple conditions (`AND`):

```
... BETWEEN 1980 AND 1999 AND genre = 'action';
```

Multiple conditions where at least one is true (`OR`):

```
SELECT * FROM movies WHERE year > 2014 OR genre = 'adventure';
```

### ORDER BY, LIMIT, DESC/ASC

`ORDER BY` sorts the results. It always precedes `WHERE`, if present.

- `ASC` sorts in ascending order (default).
- `DESC` sorts in descending order.

```
SELECT * FROM movies WHERE rating > 7 ORDER BY name;
```

```
... ORDER BY year DESC;
```

Show only 10 rows (LIMIT goes at the very end of the query):

```
SELECT * FROM movies LIMIT 10;
```

### CASE, THEN, ELSE, END

Call column `name` together with a new column `Review` which has 3 possible values (Good, Regular, Bad) that depend on the `rating`:

```
SELECT name
    CASE
        WHEN rating > 8 THEN 'Good'
        WHEN rating > 6 THEN 'Regular'
        ELSE 'Bad'
    END AS 'Review'
FROM movies;
```


## Aggregate functions

### COUNT(), SUM(), MAX/MIN()

`COUNT()` counts the number of non-empty rows in a table. It doesn’t count rows with no values.

```
SELECT COUNT(*) FROM table_name;
```

```
SELECT COUNT(*) FROM programs WHERE price = 0;
```

`SUM()` adds all the values in a certain column.

```
SELECT SUM(downloads) FROM programs;
```

`MAX()` and `MIN()` return the largest and smallest value from a column.

```
SELECT MAX(price) FROM programs;
```

```
SELECT MIN(price) FROM programs;
```

### AVG(), ROUND()

`AVG()` return the average of certain column.

```
SELECT AVG(downloads) FROM programs;
```

Return the average of the ratings of all movies of 1995:

```
SELECT AVG(rating) FROM movies
WHERE year = 1995;
```

Return the column `price` with its values rounded to 0 decimal places (by default, `ROUND()` rounds to 0 when an index is not present):

```
SELECT ROUND(price, 0) FROM programs;
```

Return the average of column `price` rounded to 2 decimal places:

```
SELECT ROUND(AVG(price), 2) FROM programs;
```

### GROUP BY

`GROUP BY` comes after any `WHERE`, but before `ORDER BY` and `LIMIT`.

Return the average ratings of each year, sorted by year:

```
SELECT year, AVG(rating) FROM movies
GROUP BY year
ORDER BY year;
```

Number of programs at each `price`:

```
SELECT price, COUNT(*) FROM programs
GROUP BY price;
```

Number of programs downloaded more than 500 times, at each `price`:

```
SELECT price, COUNT(*) FROM programs
WHERE downloads > 500
GROUP BY price;
```

Number of downloads for each `category` (the `downloads` column holds the number of downloads of each program):

```
SELECT category, SUM(downloads) FROM programs
GROUP BY category;
```

It’s possible to use **numbers to refer to columns** from the `SELECT` statement.

Number of movies per (rounded) rating, sorted by rating:

```
SELECT ROUND(rating), COUNT(name) FROM movies
GROUP BY ROUND(rating)
ORDER BY ROUND(rating)
```

```
SELECT ROUND(rating), COUNT(name) FROM movies
GROUP BY 1
ORDER BY 1;
```

Group the average of downloads by each price, and group the prices by the categories.

- 1st column: Categories.
- 2nd column: Prices for each category.
- 3rd column: Average of downloads per price per category.

```
SELECT category, price, AVG(downloads) FROM programs
GROUP BY 1, 2;
```

### HAVING

- `WHERE`: Used for limiting the results of a query based on values of individual rows.
- `HAVING`: Used for limiting the results of a query based on an aggregate property. It comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

Number of movies of different genres that are produced each year, excluding years and genres with < 10 films.

```
SELECT year, genre, COUNT(name) FROM movies
GROUP BY 1, 2
HAVING COUNT(name) >= 10;
```

Return prices grouped, average number of downloads (rounded) per price, and number of programs per price. Show only rows where number of programs per price is > 10.

```
SELECT price, ROUND(AVG(downloads)), COUNT(*) FROM programs
GROUP BY price
HAVING COUNT(*) > 10;
```


## Multiple tables

Let’s supposse we have 3 tables:

```
orders:
  order_id
  subscription_id
  customer_id
  purchase_date

subscriptions
  subscription_id
  description
  montly_price
  subscription_length

customers
  customer_id
  customer_name
  address
```

So, we have a number of customers, a number of possible subscriptions, and a number of orders made by the customers in order to acquire subscriptions.

**Primary key**: Column in a table that uniquely identifies each row. Requirements:

- None value can be `NULL`.
- Each value must be unique.
- A table cannot have more than one primary key column.

**Foreign key**: When the primary key of one table appears in a different table. When we join tables, we usually join a foreign key with a primary key.

### JOIN, ON

**Joining 2 tables**: Look some row in table A to be able to know what row to look in table B. Example: We have an order and we want to know the name of the customer that did that order, so we look `orders.customer_id` and with that datum we can find `customers.customer_name`.

Return two tables together (`orders` + `customers`), matching `customer_id` as it appears in table `orders`.

```
SELECT * FROM orders JOIN customers
ON orders.customer_id = customers.customer_id;
```

Whenever you want to specify in which table is certain column, you can use the **dot notation** (`table.column`).

Return columns `order_id` and `customer_name`, matching the latter to the first.

```
SELECT orders.order_id, customers.customer_name FROM orders JOIN customers
ON orders.customer_id = customers.customer_id;
```

Return two tables together (`orders` + `subscriptions`), matching `subscription_id` as it appears in table `orders`, but only those rows where `description` = `sport magazine`.

```
SELECT * FROM orders JOIN subscriptions
ON orders.subscription_id = subscriptions.subscription_id
WHERE subscriptions.description = 'Sport magazine';
```

If some **information is missing** in any or both tables about the columns that must be matched, the `JOIN` will only include rows that match the `ON` condition.

Example: If we join tables `customers` and `orders`, and table `customers` is missing information about customer 11, but table “orders” has an order from customer 11, when we perform a simple `JOIN` (inner join), the result will only include rows that match the `ON` condition.

Count number of rows in the resulting table of joining 2 tables:

```
SELECT COUNT(*) FROM table_1 JOIN table_2
ON table_1.id = table_2.id;
```

### LEFT JOIN

If some **information is missing** in any or both tables about the columns that must be matched, the `LEFT JOIN` will keep all rows from the first table, regardless of whether there is or isn’t a matching in the second table.

```
SELECT * FROM table_1 LEFT JOIN table_2
ON table_1.id = table_2.id;
```

```
SELECT * FROM table_1 LEFT JOIN table_2
ON table_1.id = table_2.id
WHERE table_2.id IS NULL;
```

### CROSS JOIN

`CROSS JOIN` doesn’t require an `ON` statement. You aren’t really joining any columns.

Return all the possible combinations of columns `shirts_color` and `trousers_color`:

```
SELECT shirts.shirt_color, pants.pants_color 
FROM shirts CROSS JOIN pants;
```

`CROSS JOIN` is more commonly used for **comparing** each row of a table to a list of values. Example: Compute how many users were subscribed during each month of the year.

1. Number of customers that are subscribed to the newspaper during month 3 (march):

```
SELECT COUNT(*) FROM newspaper
WHERE start_month <= 3 AND end_month >= 3;
```

2. Combination newspaper subscriptions and months (12 months per subscription):

```
SELECT * FROM newspaper CROSS JOIN months;
```

3. Return the same as point 2, but only the months where the subscriptions are active:

```
SELECT * FROM newspaper CROSS JOIN months
WHERE start_month <= month AND end_month >= month;
```

4. Return a column with the months and a column with the number of subscriptions in each month (i.e. number of appearances of each month in the previous query):

```
SELECT month, COUNT(*) FROM newspaper CROSS JOIN months
WHERE start_month <= month AND end_month >= month
GROUP BY month;
```

### UNION

Stacks `table_1` on top of `table_2`. The tables must have the same number of columns with same data types each.

```
SELECT * FROM table_1
UNION
SELECT * FROM table_2;
```

### WITH

`WITH` allows to make a separate query and then we can do whatever we want with this temporary table (such as `JOIN`). We put a whole first query inside the parentheses and give it a name. After that, we can use this name as if it is a table and write a new query using the first query.

Return a list of customers and the number of subscriptions per customer:

```
SELECT custormer_id, COUNT(subscription_id) AS 'subscriptions' FROM orders
GROUP BY customer_id;
```

From the previous query, we can use `WITH` to get, from the list `customer_id`, the names of the customers.

```
WITH previous AS (
 SELECT custormer_id, COUNT(subscription_id) AS 'subscriptions' FROM orders
 GROUP BY customer_id;
)
SELECT customers.customer_name, previous.subscriptions 
FROM previous JOIN customers
ON previous.customer_id = customers.customer_id;
```

`previous`: Alias for any columns from the query inside the `WITH` clause.


## Glossary

- `CREATE TABLE`: Creates a new table.
- `INSERT INTO`: Adds a new row to a table.
- `SELECT`: Queries data from a table.
- `UPDATE`: Edits a row in a table.
- `ALTER TABLE`: Changes an existing table.
- `DELETE FROM`: Deletes rows from a table.

- `SELECT`: Clause we use every time we want to query information from a database.
- `AS`: Renames a column or table.
- `DISTINCT`: Return unique values.
- `WHERE`: Popular command that lets you filter the results of the query based on conditions that you specify.
- `LIKE`: Special operator.
- `BETWEEN`: Special operator.
- `AND`: Combines multiple conditions.
- `OR`: Combines multiple conditions.
- `ORDER BY`: Sorts the result.
- `LIMIT`: Specifies the maximum number of rows that the query will return.
- `CASE`: Creates different outputs.

- `CREATE TABLE`: Creates a new table.
- `INSERT INTO`: Adds a new row to a table.
- `SELECT`: Queries data from a table.
- `UPDATE`: Edits a row in a table.
- `ALTER TABLE`: Changes an existing table.
- `DELETE FROM`: Deletes rows from a table.
- `COUNT()`: Count the number of rows.
- `SUM()`: Sum of the values in a column.
- `MAX()`/`MIN()`: Largest/smallest value.
- `AVG()`: Average of the values in a column.
- `ROUND()`: Round the values in the column.
- `GROUP BY`: Clause used with aggregate functions to combine data from one or more columns.
- `HAVING`: Limits the results of a query based on an aggregate property.

- `JOIN`: Combines rows from different tables if the join condition is true.
- `LEFT JOIN`: Returns every row in the left table, and if the join condition is not met, NULL values are used to fill in the columns from the right table.
- `Primary key`: Column that serves a unique identifier for the rows in the table.
- `Foreign key`: Column that contains the primary key to another table.
- `CROSS JOIN`: Lets us combine all rows of one table with all rows of another table.
- `UNION`: Stacks one dataset on top of another.
- `WITH`: Allows us to define one or more temporary tables that can be used in the final query.