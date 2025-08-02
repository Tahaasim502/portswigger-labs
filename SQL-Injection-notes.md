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

sql
Copy
Edit

Corresponding SQL query:  
```sql
SELECT * FROM products WHERE price = 100 AND released = 1;
Injection Example
URL:
https://giftswebsite.com/products?price=100'--
Becomes:

sql
Copy
Edit
SELECT * FROM products WHERE price = 100'--' AND released = 1;
The -- comments out the rest of the query, bypassing the original filter.

OR-based Injection
URL:

arduino
Copy
Edit
https://giftswebsite.com/products?price=100' OR 1=1--
Query:

sql
Copy
Edit
SELECT * FROM products WHERE price = 100 OR 1=1-- AND released = 1;
This always returns true and exposes all data.

6. Subverting Application Logic
By injecting SQL into login forms, attackers can bypass authentication:

Example input:

Username: admin' --

Password: (blank)

Query becomes:

SELECT * FROM users WHERE username = 'admin' --' AND password = '';

Password check is ignored.

---
