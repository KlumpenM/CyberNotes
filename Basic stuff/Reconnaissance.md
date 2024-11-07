Reconnaissance is also what is called **Information Gathering**, and there is two types of reconnaissance:
- Active Reconnaissance
- Passive Reconnaissance
The most important thing for reconnaissance is just to gather information. But what information might we gather, and what information are we looking for.

We are looking? (this is just some of the things we are looking for)
- Possible subdomains
- Interesting files on the web
- Breach Credentials Dumbs
	- To see if some of the emails/passwords on some of the persons works for the website we are pen testing.

# Active Reconnaissance
Active Reconnaissance is where we are doing things against the website.
We will come back to this, since this is also a part of [[Scanning and Enumeration]]

# Passive Reconnaissance
Passive reconnaissance is not doing anything *active* with the site that your are pen testing.
This is where you are gathering information about the website on sites like google, LinkedIn, the website, and other sites that might be useful for getting information about the website and the people behind the website.
It's mostly just getting a overview over the public information that's out there.
We can also split this part up into four parts, so we can define tools for each use:
- Target Validation
- Finding Subdomains
- Fingerprinting
- Data Breaches

**Target Validation**
Here we are using tools like
- WHOIS
- nslookup
- dnsrecon

There are tools that we are using to make sure that the target we are pen testing is in fact the right target. (The target is in-scope).
If we are doing bug bounty, this step can be skipped


**Finding Subdomains**
Here we are using look like
- Google Fu (passive)
- dig (passive)
- Nmap (active)
- Sublist3r (passive)
- Bluto (active)
- crt.sh (passive)
- etc

Here Sublist3r is the most recommended, since this is my go-to tool. 
But another interesting tool here is Google Fu, this can be the first thing we are checking. Google Fu functionality is instead of going to www.example.com, we don't want to stop there, we might want to go to dev.example.com or test.example.com. This can be done with Google Fu.


**Fingerprinting**
This is were we are getting into the active part of reconnaissance, were we are using both active and passive.
Here we are using tools like
- Nmap (active)
- Wappalyzer (active)
- WhatWeb (active)
- BuiltWith (passive)
- Netcat (active)


**Data Breaches**
This is where we are getting the juicy stuff, were we are getting old passwords, other passwords that might have been used on multiple accounts or across multiple websites.
Here we are using websites as:
- HaveIBeenPwned
- Other lists needs to be added.

This is not as relevant in network pen testing, but can still help. 