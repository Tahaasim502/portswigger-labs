# Lab 1: SQL Injection Vulnerability — Retrieving Hidden Data

## Lab Overview

This lab focuses on exploiting a SQL injection vulnerability in the WHERE clause that allows an attacker to retrieve hidden or unauthorized data from a web application.

## Key Concepts Learned

- How unsanitized user input can manipulate SQL queries.
- Using payloads like `' OR 1=1--` to bypass filtering conditions.
- Understanding the impact of injection on data exposure.
- Importance of securing queries via parameterization and input validation.

## Solution

The SQL injection payload used to bypass the filter was:

```sql
[SQL Injection Exploit](https://0a9d00610413b58b801e0d1700e200ec.web-security-academy.net/filter?category=Gifts%27+OR+1=1--)
'OR 1=1--
```
