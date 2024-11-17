# What is it
There is different types SQL Injection:
- d
- Blind SQL injection

# How to do it?
The most simple form of SQL Injection, is in a login form, or submit form with the inputs (in the all the input fields):
```
'
```
If this gives us an error or something like `[object Object]` we have an error where we can use SQL injection.
We can further inspect this with [[Burp Suite]] and its repeater. If we get a 500 internal server error and seeing SQL error statements, we have a SQL injection, and we start to Fuzz the parameter that gives us the SQL injection.


# Tools to use
There is a broad range of tools, to either identify and test/exploit the injection.
**Identify**:
- Burp Suite

**Test/Exploit**:
- Burp Suite
- SQLmap