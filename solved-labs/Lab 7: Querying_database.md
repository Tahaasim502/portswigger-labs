# Lab 7 : SQL Injection Attack – Querying Database Type and Version (MySQL & Microsoft)

## Lab Overview

This lab contains a **SQL injection vulnerability** in the product category filter. The vulnerability allows using a **UNION attack** to inject and retrieve data from the database.

## Objective

To solve the lab, you need to display the **database version string** using SQL injection.

---

## How I Solved the Lab

- Found the injection point in the product category filter.
- Tested the number of columns to match the original query.
- Used a UNION SELECT query to retrieve the database version string:


## Solution:

<img width="1283" height="599" alt="Screenshot (780)" src="https://github.com/user-attachments/assets/f812aaed-e35f-4575-9be9-07211eb44498" />

```sql
  ' UNION SELECT @@version--+
```
