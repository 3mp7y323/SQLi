# SQLi
SQL – injection
- [1. What is SQLi? Why does SQLi exist?](#1-what-is-sqli-why-does-sqli-exist)
  - [1.A) What is SQLi?](#1A-What-is-SQLi)
  - [1.B) Why does SQLi exist?](#1B-Why-does-SQLi-exist)
    - [a. Improper handling of input data](#a-improper-handling-of-input-data)
    - [b. Lack of using prepared statements and parameterized queries](#b-lack-of-using-prepared-statements-and-parameterized-queries)
    - [c. Using insecure APIs](#c-using-insecure-apis)
    - [d. Lack of security awareness](#d-lack-of-security-awareness)
    - [e. Lack of security testing procedures](#e-lack-of-security-testing-procedures)
    - [f. Outdated or insecure infrastructure](#f-outdated-or-insecure-infrastructure)
  - [1.C) Types of SQLi](#1C-Types-of-SQLi)
    - [a. In-band SQLi:](#a-In-band-SQLi)
    - [b. Inferential (Blind) SQLi:](#b-Inferential-Blind-SQLi)
    - [c. Out-of-band SQLi:](#c-Out-of-band-SQLi)
- [2. The level of damage caused by SQLi!!!](#2-The-level-of-damage-caused-by-SQLi)
- [3. How SQLi works. Tools used for exploitation. Remediation.](#3-How-SQLi-works-Tools-used-for-exploitation-Remediation)

## 1. What is SQLi? Why does SQLi exist?
### 1.A) What is SQLi?
![image](https://github.com/thienusa2000/SQLi/assets/55008350/59a22032-f2c5-4cfd-ba9f-159807af9fc2)

- Before diving into SQLi, let's first understand SQL. In simple terms, SQL (Structured Query Language) is a language designed to manage and manipulate data in relational database management systems (RDBMS).
- SQLi, or SQL injection, is simply the act of injecting SQL commands into any input channel to send malicious commands, including <input> tags, query strings, cookies, and files. For example, when logging in, in the username and password fields, we can inject an SQL statement like:
"SELECT * FROM users WHERE username = 'user' OR '1'='1' AND password = 'anything';"
- Because the condition OR '1'='1' is always true, this query will return all records in the users table, allowing attackers to log in without a valid password.
- In summary, SQLi is a security attack technique in which attackers exploit vulnerabilities in web applications to inject malicious SQL statements into valid SQL queries. The goal is to access or manipulate data in the database illegally.

### 1.B) Why does SQLi exist?
a. Improper handling of input data:
   - Lack of input data validation and sanitization.
   - Directly concatenating strings into SQL statements.
b. Lack of using prepared statements and parameterized queries:
   - Prepared statements and parameterized queries ensure that input data is treated as data, not SQL code. Without using this technique, systems are vulnerable to attacks via malicious input.
c. Using insecure APIs:
   - Some APIs or outdated libraries do not support or encourage modern security measures, making applications vulnerable to attacks.
d. Lack of security awareness:
   - Programmers lack knowledge of security methods or fail to adhere to best security practices when developing applications.
e. Lack of security testing procedures:
   - Failure to perform comprehensive security testing procedures during software development, including source code review and application security testing.
f. Outdated or insecure infrastructure:
   - Using outdated versions of database management systems or other software components without security patches.

### 1.C) Types of SQLi
We can classify the 8 types of SQL Injection into 3 main groups: In-band SQLi, Inferential (Blind) SQLi, and Out-of-band SQLi.

#### a. In-band SQLi:
   - Error-Based SQLi: Attackers retrieve information from the database through SQL error messages.
   - Union-Based SQLi: Using the UNION operator to combine results from different SQL statements and retrieve information from the database.

#### b. Inferential (Blind) SQLi:
   - Boolean-Based SQLi: Using logical expressions (TRUE or FALSE) to gather information from the database.
   - Time-Based SQLi: Using SQL statements to delay responses to determine the existence of data or extract information from the database sequentially.
   - Blind SQLi (Error-Based or Time-Based): Attackers do not receive SQL error messages or direct information from the database, but they can still determine information by observing application behaviors or response times.

#### c. Out-of-band SQLi:
   - Out-of-band SQLi (OOB): Using functions or features dependent on other protocols such as DNS or HTTP to transmit data from the database outward.

## 2. The level of damage caused by SQLi!!!
SQL Injection (SQLi) is one of the most serious security vulnerabilities, and the damage it can cause is diverse and severe. Here are the main levels of damage that a SQLi attack can cause:

1. Sensitive information disclosure:
   - Attackers can access sensitive data such as usernames, passwords, email addresses, personal information, and even financial information from the database.
   - Example: An attack on an e-commerce website could expose customers' credit card information.

2. Data alteration or deletion:
   - Attackers can alter or delete data in the database, leading to loss of important data or data distortion.
   - Example: Changing product prices in an online store or deleting important transaction records.

3. Injection of additional malicious data:
   - Attackers can insert malicious or fake records into the database.
   - Example: Adding fake user records or spam comments to the system.

4. System control takeover:
   - In some cases, attackers can use SQLi to take control of the database server or even the application server.
   - Example: Executing system commands or accessing sensitive files on the server.

5. Complete database destruction:
   - An SQLi attack can lead to the complete destruction of the entire database, causing service disruptions and significant data and financial losses.
   - Example: Deleting all tables and data in the database of a financial organization.

6. Denial of Service (DoS) attacks:
   - Attackers can overload the system by performing complex or inefficient queries, leading to denial of service attacks.
   - Example: Performing network-clogging queries or consuming all server resources.

7. Reputation and customer loss:
   - A successful SQLi attack can cause serious reputation damage to the organization and loss of trust from customers.
   - Example: If customers' personal data is exposed, they may stop using the service and switch to competing providers.

8. Legal costs and fines:
   - Organizations may face legal action and fines if they fail to protect customers' personal data according to legal regulations.
   - Example: Violating GDPR (General Data Protection Regulation) regulations can lead to hefty fines for organizations operating in Europe.

Real-life examples of famous SQL Injection attacks:

1. Heartland Payment Systems (2008):
   - One of the largest SQLi attacks in history, exposing over 130 million credit card numbers. The company incurred millions of dollars in losses due to fines and remediation costs.

2. Target (2013):
   - Although not an SQLi attack, a security vulnerability led to the theft of 40 million credit and debit card information. Remediation costs amounted to hundreds of millions of dollars.

3. Sony Pictures (2014):
   - An SQLi attack allowed attackers to access the database and steal sensitive information, including emails and financial information. This event caused significant financial and reputational damage to Sony.

Thus, the damage caused by SQL Injection can be very serious and diverse, affecting data, finances, reputation, and even legal aspects of organizations. Therefore, preventing and protecting systems from SQLi attacks is extremely important.

## 3. How SQLi works. Tools used for exploitation. Remediation.
### A) How SQLi works.
   - When a web application receives data from users (such as from input forms, URLs, or query parameters), if that data is not properly processed and validated, attackers can inject malicious SQL code into this input. This malicious SQL statement is then sent to the database for execution.

### B) Tools used for exploitation
a. SQLMap:
   - SQLMap is one of the most popular tools for automating the detection and exploitation of SQLi vulnerabilities.
   - Features: Automatically detects database types, injects malicious code, retrieves data, and executes system commands.
b. Havij:
   - Havij is a powerful SQLi exploitation tool with a user-friendly interface, popular in the hacker community.
   - Features: Automatically detects and exploits vulnerabilities, extracts data, and performs advanced attacks.
c. Burp Suite:
   - Burp Suite is a comprehensive toolkit for web application security testing.
   - Features: Burp Scanner has the ability to detect SQLi, in addition to having Intruder and Repeater for customization and exploitation of vulnerabilities.
   - Usage: Burp Suite Community Edition (free) and Burp Suite Professional (paid).

d. SQLNinja:
   - SQLNinja focuses on exploiting SQLi vulnerabilities on Microsoft SQL Server.
   - Features: Exploits SQLi to take control of the server, execute system commands, and initiate reverse shells.

e. BBQSQL:
   - BBQSQL is a brute force tool for exploiting SQLi based on Blind SQL Injection.
   - Features: Particularly useful for Blind SQLi scenarios, where query results are not displayed directly.

f. jSQL Injection:
   - jSQL Injection is a Java tool for exploiting SQLi, supporting multiple types of databases.
   - Features: Supports multiple SQLi techniques and has a user-friendly graphical interface.

   These SQLi exploitation tools are powerful and useful for security professionals in detecting and remedying vulnerabilities. However, their usage should be done responsibly and in compliance with legal regulations.

### C) Remediation:
To address SQL Injection vulnerabilities (SQLi), you can implement the following concise measures:

1. Use Prepared Statements and Parameterized Queries:
   - Ensure that SQL statements are prepared in advance and input parameters are handled separately.

2. Use ORM (Object-Relational Mapping):
   - Utilize ORM frameworks to automate the creation of safe SQL queries.
   - Example: Use SQLAlchemy for Python, Hibernate for Java.

3. Validate and Sanitize Input Data:
   - Validate and sanitize all input data to ensure they only contain valid characters.
   - Use data sanitization functions or available libraries.

4. Limit Database Permissions:
   - Grant minimal necessary permissions to database access accounts.
   - Example: Query accounts should not have permission to alter database structure.

5. Use Secure APIs:
   - Utilize modern APIs or libraries that support security measures, such as PDO (PHP Data Objects) for PHP.

6. Regularly Update and Patch:
   - Ensure that systems and related software are always updated with the latest security patches.

7. Perform Regular Security Testing:
   - Conduct regular application security testing, including penetration testing and vulnerability scanning.

8. Use Web Application Firewall (WAF):
   - Deploy a WAF to block SQLi attacks before they reach the application.

By implementing these measures, you can minimize the risk of SQL Injection attacks and effectively protect your application.
