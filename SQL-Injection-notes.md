```sql
🧠 SQL Injection — Notes & Understanding

📌 1. What is SQL Injection?

SQL Injection is a vulnerability that occurs when an attacker can manipulate the SQL queries that an application sends to the database. This can lead to:

- Unauthorized data access

- Data manipulation

- Authentication bypass

In severe cases, full system compromise

🌐 2. Understanding Web Applications
Web apps are usually database-driven. They operate across 3 core layers:

Presentation Layer: The front-end (browser/UI)

Logic Layer: Backend server logic (e.g., Node.js, PHP)

Storage Layer: The database (e.g., MySQL, MSSQL)

⚙️ How They Work
When a user interacts with the app (e.g., filters products):

The browser (presentation layer) sends the request

Backend (logic layer) handles it and queries the database

The database (storage layer) returns relevant data

🛍️ Example: On an e-commerce site, filtering by price:

SELECT * FROM products WHERE price = 50 AND released = 1
🔄 3. Evolving to Four-Layer Architecture
Many modern apps now use a 4-layer architecture, adding an API layer between logic and storage:

This API layer (Application Programming Interface) manages communication and business logic.

Benefits: Scalability, separation of concerns, code reuse.

🧪 4. How to Detect SQL Injection
Test with ' (single quote) to trigger errors

Use Boolean payloads:
OR 1=1, OR 1=2

Look for vulnerable SQL statements:

WHERE, SELECT, INSERT, UPDATE, ORDER BY, etc.

📥 5. How SQL Queries Work with User Input
Given:
https://giftswebsite.com/products?price=100
The backend might run:

SELECT * FROM products WHERE price = 100 AND released = 1
🚨 Injected Variant

https://giftswebsite.com/products?price=100'--
Becomes:

SELECT * FROM products WHERE price = 100'--' AND released = 1
-- comments out the rest of the query, potentially bypassing logic.

✅ OR-Based Injection
https://giftswebsite.com/products?price=100'+OR+1=1--
Yields:
SELECT * FROM products WHERE price = 100 OR 1=1-- AND released = 1

🚪 6. Subverting Application Logic
You can bypass login forms by injecting SQL into the login fields.

For example:

Username: admin' --

Password: (left blank)

The query becomes:

SELECT * FROM users WHERE username = 'admin' --' AND password = ''
```
SELECT * FROM users WHERE username = 'admin' --' AND password = ''
This bypasses password checks entirely.
