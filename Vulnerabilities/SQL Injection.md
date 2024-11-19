# What is it
SQL injection (SQLi) is a vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allows an attacker to view data that they are not normally able to retrieve. This might include data that belongs to other users, or any other data that the application can access.
In some situation a SQL injection attack can be escalated into a compromise of the underlying server, or other back-end infrastructure.
We can also use SQL injection to preform [[Denial-of-service]]
attacks.

There different types SQL Injection:
- First-order SQL injection
	- It occurs when the application processes user input from an HTTP request and incorporates the input into a SQL query in an unsafe way.
- Second-order SQL injection (stored SQL injection)
	- It occurs when the application takes uses input from an HTTP request and stores it for future use. This is usually done by placing the input into a database, but no vulnerability occurs at the point where the data is stored. Later, when handling a different HTTP request, the application retrieves the stored data and incorporate it into a SQL query in an unsafe way. That's why we call it "Stored SQL injection"
- Blind SQL injection

Here are some common SQL verbs, that we typically use when trying to perform SQL injection:
- SELECT - Retrieves data from a table
- INSERT - Adds data to a table
- DELETE - Removes data from a table
- UPDATE - Modifies data in a table
- DROP - Deletes a table
- UNION - Combines data from multiple queries
- WHERE - Filters record based on specific condition
- AND/OR/NOT - filter records based on multiple conditions
- ORDER BY - Sorts record in ascending/descending order

But there is sometimes where we need to use more than the common verbs in SQL, we also need to introduce special characters in order to bypass some filters:
- ' and " - String delimiters 
- --, /* and # - Comment delimiters
- * and % - Wildcards
- ; - Ends SQL statement
- Logic operators: =, +, <, >, (), etc.

# How to do it?
The most simple form of SQL Injection, is in a login form, or submit form with the inputs (in the all the input fields):
```
'
```
If this gives us an error or something like `[object Object]` we have an error where we can use SQL injection.
We can further inspect this with [[Burp Suite]] and its repeater. If we get a 500 internal server error and seeing SQL error statements, we have a SQL injection, and we start to Fuzz the parameter that gives us the SQL injection.
Another simple injection we can test is this (if we are allowed to create users on the web app)
```
username' OR 1=1; --
```
This will give us information about the underlying database structure, or logs us in as the first item in the database (usually the admin account)

# Tools to use
- Burp Suite
- SQLmap
- NoSQLMAP
- 