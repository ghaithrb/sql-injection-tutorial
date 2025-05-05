# SQL Injection Tutorial

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

---

## What is SQL Injection?

SQL Injection is a **code injection technique** that exploits vulnerabilities in an application’s software by manipulating SQL queries. It allows attackers to **interact with the database** in unauthorized ways — retrieving data, bypassing logins, or even dropping tables.

---

## How It Works

Consider this SQL query:

```sql
SELECT * FROM users WHERE username = '$username' AND password = '$password';

##If an attacker enters the following:
' OR '1'='1

