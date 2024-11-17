# What is it
There are three different types of Cross-site Scripting and we can utilize them all three differently:
- DOM XSS
- Reflected XSS
- Stored XSS
Just remember that for DOM based and Reflected we need phishing or some sort of social engineering aspect, since we need the admin or high privileges users to click or malicious link, where we don't need to do that in the stored case.

### DOM
DOM is the "Document Object Model" that provides the object oriented representation of the html documents.
The DOM can be used to generate dynamic content, this can we utilize to get malicious intent.
DOM based can be very hard to wrap ones head around, but just think of it as **reflected**, since they are very close, but just a bit different in the way that they are handled.
Since the DOM has a "source" and a "sink", when a user inputs malicious code, that's called the "source", and where the code is executed its called the "sink". 
To get more information, read this [article](https://www.scip.ch/en/?labs.20171214), it describes it perfectly.


### Reflected (Client side)
Reflected is typically the first one of them that we are testing for, this is where we are entering a payload into a website, and a alert comes up (if the payload is: `alert('XSS')`, which is the most common).
It doesn't get sent to the server, that's why it only happens client side.
If we want it to be stored on the server, we must exploit a "stored XSS"

### Stored
Stored is when we, as an example, have a script or payload stored in a comment or something on the page, when another user clicks the script or link, the JavaScript gets triggered. Therefor it gets stored on the server.


# How do we do it?
To know how we do it, we must first understand how XSS works, both on the client side, and the server site. 
**example**:
Let's say that we have a PHP document: `index.php`, and it might look like this:
```
<?php
%username = $_GET['username']
echo "Hi $usernamae"
?>
```
Then if we could control the parameter `username` in the URL, we could change the username like this: `index.php?username=ruben`, it would come back with: `Hi ruben`.
What if we did something malicious like:
```
username=<script>alert('1')</script>
```
That should give us a alert on the page with the text "1".
This is a **very basic** example, but it's just for understanding the concept of XSS. 

**Bypassing sanitization**
When it comes to XSS, there is a lot of filtering on most of the websites in the wild. Therefore we need to be creative when it comes to trying to bypass the validation of a input, if we can bypass the sanitization.
Lets say that we have a input where if we type: `<script>alert('xss')</script>` it display `lert('xss')</script>` on the page, here we can see that something is getting sanitized, but not all of the input is getting sanitized.
Here we need to get creative in order to bypass, and this is where we are going for bitwise operators, to see if this XSS can be exploited, we can input:
```
<<a|ascript>alert('xss')</script>
```
If this gets through, it's because it starts to sanitize the first part, and gets to the expression: `a|a` where we are having the "OR", and since this is the gets validated to 1 -> True, and it executes the rest of the code, therefore resulting in a stored XSS.
Here we just choses the "OR" operator, but we can use all the other bitwise operators.

# Tools
- Burp Suite (Manually or Intruder)
- XSSer

# Mitigations
**Encoding:**
When we are doing encoding to scripts, we can mitigate the execution of scripts, this means that when we are seeing this:
```
<script>
```
We should encode it such that:
```
< == &lt;
```
This means that every time we see a `<` it gets converted into `&lt;` when it hits the server, which is the escape sequence  of the symbol.

**Filtering**:
This is also a technique we can use to mitigate XSS, this is where, when we are seeing:
```
<script>
```
It gets converted into:
```
script
```
So we are just removing the "<" and ">", so it doesn't get executed on the server:

**Validation**
This is just a comparison against a list, so that every time we see a "script" tag, we eliminate these. So we are removing the tags. We are looking at a list, before it hits the server, and running it on the server.
There are predefined lists, that we can use.

**Sanitization**
This is a combination of all the above techniques. 