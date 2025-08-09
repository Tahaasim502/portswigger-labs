## 📂 What is Path Traversal?

Also known as Directory Traversal.

It allows attackers to access arbitrary files on the server running the application, such as:

- Application code and data

- Backend system credentials

- Sensitive operating system files

If attackers access these files, they can modify them and potentially take control of the system or server.

----

## 🔍 Reading Arbitrary Files via Path Traversal
Example of a vulnerable site:

```html
<img src="/loadImage?filename=218.png">
```

How it works:

The loadImage endpoint takes a filename as a parameter and returns that file’s contents.

On disk, the file might be located at:

```sql
/var/www/images/218.png
```

Without protections, an attacker can manipulate the filename parameter to traverse directories and read sensitive files:
```sql
/var/www/images/../../../etc/passwd
```
Here, each ../ moves one directory level up. Using it three times goes up three levels to access /etc/passwd.

Example exploit URL:
```sql
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```
---

## 🚧 Common Obstacles & Bypass Techniques

Sometimes the app or server strips or blocks the ../ traversal sequences.

To bypass this, attackers can use:

Nested traversal sequences like ```....//``` or ```....\/```. When the app strips the inner part, it effectively becomes ../.

URL Encoding can bypass filters:

../ becomes %2e%2e%2f (. → %2e, / → %2f). Some servers fail to detect this and allow traversal.

Double URL Encoding:

Encoding % signs as well: %252e%252e%252f. This can bypass filters if the server decodes input twice.

Absolute paths can sometimes be used directly (if known), e.g., /var/www/images/../../../etc/passwd.

Some systems require a file extension; attackers may append null byte injection to bypass checks:
```sql
../../../etc/passwd%00.png
(%00 acts as a string terminator in some environments)
```

---

## 🛡️ How to Prevent Path Traversal Attacks

- Validate and Sanitize User Input
  - Only allow safe characters or a whitelist of filenames/paths.

- Never Trust User Input
  - Always treat user data as potentially dangerous.

- Use Safe File Handling Functions
  - Use built-in language or framework functions that handle paths securely instead of manual string concatenation.

Store Sensitive Files Securely
Keep important files outside the web root or restrict access via server configuration.
