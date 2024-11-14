## What is Burp Suite
**Burp Suite** is a proprietary software tool for security assessment and penetration testing of web applications. We are using it, when we are **actively** scanning a website
Burp suite both exists as a free version and a paid version. 
- The paid version is around 450$, which is a lot but truly worth it. Since it allows for extensions


# Scanning a website
When we are scanning with Burp Suite, we are actively scanning the website. Even though we think that we are scanning the whole website, we are only scanning $\approx 50\%$ of the website or Burp Suite is touching around that much of the website.
- Therefore we need to manually crawl the site, so that burp can see the rest of the site.
Also when we are scanning the website, and done manually crawling the website we can do the scan.
But when we are scanning a website it **doesn't pick up all the things**, it gives us a overview of what **might** be wrong/misconfigured on the website, but it can also give us a lot of **false positives**.

## Manual work
We want to make a lot of manual request to the website, submitting buttons, search queries.
- Just getting a lot of parameters in the url, and the request.


## Extensions
Extensions are available for both the free version and the paid version of Burp Suite, but most of the useful (doesn't say that the free plugins are useless) plugins are **only** for the paid version.
Here is a list of some of the extensions that I've installed:
- Active Scan++
- Retire.js
- J2EEScan
- Authorize
- JWT tokens 