# Lab 4: SQL Injection — Finding Columns Containing Text

## Lab Overview

This lab focuses on identifying which columns in a SQL query can display string data. This is crucial for displaying injected data like usernames or passwords via a UNION-based attack.

---

## Key Concepts Learned

- Not all columns accept or render text.

- Using UNION SELECT with strings like 'a', 'b', etc., to detect text-compatible columns.

- Leveraging reflected values in the web page to confirm success.

- A necessary step before extracting real data in UNION attacks.

---

## Solution

<img width="1303" height="589" alt="Screenshot (769)" src="https://github.com/user-attachments/assets/0df76271-8886-4caf-a05a-39938539d727" />


```sql
'UNON SELECT NULL,'2VKil8',NULL--
```
