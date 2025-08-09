# Lab 1: File Path Traversal - Simple Case

## 📝 Description

This lab focuses on exploiting a basic **File Path Traversal** vulnerability.  
The application accepts a filename parameter and loads files from the server without proper validation or sanitization, allowing traversal to sensitive files outside the intended directory.

## 🎯 Objective

- Understand how to manipulate file path inputs to access arbitrary files on the server.  
- Learn how directory traversal sequences like `../` can be used to move up directories and access protected system files.  
- Practice exploiting the vulnerability by reading files such as `/etc/passwd`.

## Solution

<img width="1365" height="471" alt="Screenshot (794)" src="https://github.com/user-attachments/assets/8dcff959-0003-4f96-a1e9-ae315221168f" />

```
<img src ="/image?filename=../../../etc/passwd"
```
