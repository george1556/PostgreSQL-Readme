# SQL Reference Sheet

## Creating a Database

```sql
-- Syntax:
CREATE DATABASE databasename;

-- Example:
CREATE DATABASE testDB;
```

## Creating a Table

```sql
-- Syntax:
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);

-- Example:
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

## How to get everything from a single table

The SELECT statement is used to select data from a database.
The data returned is stored in a result table, called the result-set.

```sql
-- Syntax:
SELECT * FROM table_name;

-- Example:
SELECT * FROM Customers;
```

## How to get one thing from a single table using "where"

The WHERE clause is used to filter records.
The WHERE clause is used to extract only those records that fulfill a specified condition.

```sql
-- Syntax:
SELECT column1, column2, ...
FROM table_name
WHERE condition;

-- Example:
SELECT * FROM Customers
WHERE Country='Mexico';
```

## How to add something inside of a table

```sql
-- Syntax:
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

-- If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. However, make sure the order of the values is in the same order as the columns in the table. The INSERT INTO syntax would be as follows:
INSERT INTO table_name
VALUES (value1, value2, value3, ...);

-- Example:
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

## How to edit something inside of a table

```sql
-- Syntax:
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- Example:
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```

## How to remove something from a table

```sql
-- Syntax:
DELETE FROM table_name WHERE condition;

-- Example:
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';
```

## What is a join statement? Why would we use a join statement?

A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

Here are the different types of the JOINs in SQL:
**\*(INNER) JOIN:** Returns records that have matching values in both tables
**\*LEFT (OUTER) JOIN:** Returns all records from the left table, and the matched records from the right table
**\*RIGHT (OUTER) JOIN:** Returns all records from the right table, and the matched records from the left table
**\*FULL (OUTER) JOIN:** Returns all records when there is a match in either left or right table

![alt text](https://www.w3schools.com/sql/img_innerjoin.gif "Inner Join") ![alt text](https://www.w3schools.com/sql/img_leftjoin.gif "Left Join") ![alt text](https://www.w3schools.com/sql/img_rightjoin.gif "Right Join") ![alt text](https://www.w3schools.com/sql/img_fulljoin.gif "Full Outer Join")

Example Tables:

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 10308   | 2          | 1996-09-18 |
| 10309   | 37         | 1996-09-19 |
| 10310   | 77         | 1996-09-20 |

| CustomerID | CustomerName                       | ContactName    | Country |
| ---------- | ---------------------------------- | -------------- | ------- |
| 1          | Alfreds Futterkiste                | Maria Anders   | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Mexico  |
| 3          | Antonio Moreno Taquería            | Antonio Moreno | Spain   |

```sql
-- Example using data from tables above:
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

Will Produce something like this:

| OrderID | CustomerName                       | OrderDate  |
| ------- | ---------------------------------- | ---------- |
| 10308   | Ana Trujillo Emparedados y helados | 9/18/1996  |
| 10365   | Antonio Moreno Taquería            | 11/27/1996 |
| 10383   | Around the Horn                    | 12/16/1996 |
| 10355   | Around the Horn                    | 11/15/1996 |
| 10278   | Berglunds snabbköp                 | 8/12/1996  |
