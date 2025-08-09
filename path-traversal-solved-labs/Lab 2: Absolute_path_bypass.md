# Lab: File Path Traversal - Traversal Sequences Blocked with Absolute Path Bypass

## 📝 Description

This lab demonstrates a File Path Traversal vulnerability where the application attempts to block `../` sequences, but the restriction can be bypassed by supplying an absolute path to the target file.

Instead of using relative directory traversal `(../)`, an attacker can directly request files from the filesystem by specifying their full path, effectively bypassing the filtering mechanism.

## 🎯 Objective

- Understand how absolute paths can bypass directory traversal filters.

- Learn why filtering only `../` is insufficient as a security measure.

- Successfully retrieve sensitive files such as /etc/passwd.

## Solution

<img width="1366" height="424" alt="Screenshot (795)" src="https://github.com/user-attachments/assets/3309a3ab-eeee-4cb9-a740-8099df872193" />
```
<img src ="/image?filename=/etc/passwd"
``
