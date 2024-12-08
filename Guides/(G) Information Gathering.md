Imagine this scenario:
- We are tasked with gathering information about a website, and get as much information about the website as possible.

The first thing that we need to make sure is what URLs that are "**in-scope**" and "**out-of-scope**".
This means what website are we allowed to search for vulnerabilities and what we are not allowed to do.

The first tools that we are going to use is my go-to tool: **Sublist3r**, that can be found [here](https://github.com/aboul3la/Sublist3r). 

To run Sublist3r use the following command:
```
sublist3r -d <domain>
```
If it's not installed it's in the apt package manager, so we can just run the command to install it
```
sudo apt install sublist3r
```

**Output**:
This is going to give us a very detailed 


# Crt.sh
We can also use the website [crt.sh](https://crt.sh/), this is also for information gathering.
Here we can type in the following:
```
%.<domain>
```

Here the `%` is acting as a **wildcard** operator, so we are getting information about all the available subdomains.
Here we are looking for interesting subdomain, that can gives us more information such as VPN services, Active Directory (AD) domains, Mail exchange domains, Slack, Jira, etc. 
The more that we find interesting, the more we can attack.


# Burp suite
We can also use Burp suite, for information gathering. This can be hard as a beginner, since it's very overwhelming in its functionality. But this is a great tool to invest time in, and money (if necessary), since the pro edition is 450$

**Setting up** (Recommended)
To configure Burp suite the right way, the first time we can do one of two things:
- Setting up a local proxy in your browser (easy for Firefox users)
	- Setting up a HTTP proxy: 127.0.0.1:8080
- Install a add-on called FoxyProxy (download [here](https://getfoxyproxy.org/))
	- This can be done for both Firefox and chrome.
	- This is in stead of opening the Burp Suite browser all the time.

**Intercepting (active)**
The main thing that we use Burp suite for as a Berninger is analysing request (GET, POST, DELETE), if this doesn't sound familiar to you, read about it [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).
When we go to the site that we are testing, we can see in Burp suite that we are getting a lot of different request.
- This can seem overwhelming at first, but we can filter all the requests we are looking at by a simple feature in Burp Suite.
We do this, by adding the website we are looking at to the filter *in scope*. This should get all the requests into a manageable sense.

**Scope**
A thing we can do in Burp Suite, is that we can use advance scopes, meaning that we can not only match on a specific web address, but we can match on Regex instead, giving us a broader view of the website, and what requests that's going in and out of the website we are testing. This pattern is the one that I use: `.*\.test\.com$`, where "test", is the website that we are testing.
This scope change, enhances the scope so that instead of only seeing "test.com", we see all the wildcard subdomains of the website we are testing.

**Scan** vs **auditing**
When it comes to Burp Suites options for either scanning a website vs auditing a website, is means two different things:
Scanning:
- Scanning means that we are scanning the website, for what could be vulnerabilities, but we **are not exploiting** them.
Auditing:
- Auditing is also a form of scanning the website, for what could be vulnerabilities, but we **are trying to exploit** them.
But since we are scanning the website, we are not doing anything actively. So we are not going to exploit anything *yet*. We are for the most part only seeing information about the header, and misconfigurations in the header

**Files**
When we are scanning a website, we are mainly looking for **asp, aspx, asm, amx**
When we are doing exploit we are looking for **boot.ini**, so the server information is critical.

# Caido
Caido is like Burp Suite enter price model, but it's free.
*details comming later....*


# Securityheader.io
This is a website, that gives us information about the website headers, keep in mind that this is just a informal website, that does a quick scan of the website **and not a deep scan**.
It gives us a overall summary of what should be on the headers of the standard request.
- When doing a pen test of a website, we can take the information of the securityheader.io (the missing headers) and put it into a **report as a low finding**. (more in the [[Report notes]])
This is something we are looking for, but not worrying about at the moment.


# Wappalyzer
Wappalyzer is a must use website, or a must have extension in Google Chrome or Firefox. It gives us useful information, such a JavaScript framework, server information, CMS, CND, etc.
- This is also something we should be able to see in the headers information
If we see information such as server information and server version, it would be a **low finding** in a pen test report, look for more in the [[Report notes]].


# Builtwith
[Builtwith](https://builtwith.com/) is a site like [[#Wappalyzer]], where we are also getting information about what the site and the underlying structure of a website is like.


# We leak info
[We leak info](https://weleakinfo.io/) is a paid website (2$ for 24 hours), which returns information from database breaches and other leaks.
This is where we are can search for the following:
- Email
- Username
- Email By Password and Username by Password
- Phone
- Domain 
- Email by hash
This will return anything that matches the search, that has been in a breach. By using these credentials, we can use them for [[Credentials stuffing]] or [[Passwords spraying]].


# Hunter.io
This is also a website where we can look up, the website that we are testing. 
This can give us patterns like:
- Email pattern
	- Which can be helpful for credentials stuffing and password spraying
	- Or just plain brute-force attacking the website.
With the email pattern, we can check the email pattern or account against an outlook server.
**Caution:** This can cause the person to be locked out, if we just spray and pray over and over again.