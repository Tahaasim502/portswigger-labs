# Lab 3: Determining Number of Columns in SQL Injection UNION Attack

## Lab Overview

This lab demonstrates how to find the number of columns returned by a SQL query to perform a successful UNION-based SQL injection.

---

## Key Concepts Learned

- Using ORDER BY clause to identify the number of columns.

- Crafting UNION SELECT statements with matching column counts.

- Injecting test values to confirm visible columns.

- Importance of matching column count for UNION injection to work.

---

## Solution

The approach involved incrementally testing:

```sql
' UNION SELECT NULL,NULL,NULL--
```
