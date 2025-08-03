# Lab 5: SQL Injection — Retrieving Data Using UNION Attack

## Lab Overview

This lab demonstrates how to use a UNION-based SQL injection to retrieve data from other tables in the database, such as usernames or email addresses.

---

## Key Concepts Learned

- UNION can combine results from the original query with attacker-supplied data.

- Requires matching the number and type of columns.

- Helps retrieve sensitive data (e.g., from users table).

- Must display text through a visible column.

---

## Solution

<img width="1272" height="553" alt="Screenshot (771)" src="https://github.com/user-attachments/assets/a6b7cef7-bfed-40d3-877e-79df02fb7609" />

<img width="1275" height="531" alt="Screenshot (770)" src="https://github.com/user-attachments/assets/9aebe801-4ad0-4e32-bbf4-3ea91bf8bdba" />

```sql
'UNION SELECT username,password FROM users--
```
