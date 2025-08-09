# Lab: File Path Traversal – Validation of File Extension with Null Byte Bypass

## 📝 Description

This lab features a File Path Traversal vulnerability where the application validates file extensions to block malicious files.

However, using a null byte (%00) injection allows bypassing this extension check, tricking the app into accepting unauthorized files.

## 🎯 Objective

- Understand how null byte injection terminates strings early in some languages.

- Bypass file extension validation using %00 to access restricted files.

- Retrieve sensitive files such as /etc/passwd.

## Solution

<img width="1364" height="437" alt="Screenshot (799)" src="https://github.com/user-attachments/assets/79f11529-a7bf-428e-b377-8f1760ddaac2" />

```
<img src="/images?filename=../../../etc/passwd%00.png">
```
