# What is it?
A **Web Application Firewall (WAF)** is a security system that monitors, filters, and blocks malicious HTTP/S traffic to and from a web application. Unlike traditional firewalls that protect networks at the transport level (OSI layers 3 and 4), a WAF focuses on the application layer (OSI layer 7) of the [[OSI Model]].
It is specifically designed to defend against web application attacks such as:
- [[SQL Injection]]
- [[Cross-site Scripting (XSS)]]
- [[Cross-Site Request Forgery (CSRF)]]
- [[File Inclusion Attacks]]
- Distributed Denial of Service (DDOS) for application layers

# How is WAF used?
1) **Mitigation of OWASP Top 10 Threats**: A WAF protects applications from common vulnerabilities output by OWASP (e.g., SQL Injection, XSS).
2) **Traffic Filtering**: IT examines incoming traffic based on predefined rules, identifying and blocking suspicious activities.
3) **DDoS Protection**: Many WAFs also provide features to mitigate application-layer DDoS attacks, ensuring consistent application availability.
4) **Compliance**: Organization often use WAFs to comply with regulatory requirements like PCI, DSS, which mandate the protection of web applications.
5) **Monitoring and Alerts**: WAFs provide logging and alerts, helping administrators detect and responds to attacks in real-time.

# How is a WAF implemented?
1) **Deployment Modes**:
	- **Inline Proxy (Reverse Proxy)**: The WAF sits between users and the application server, intercepting and inspecting traffic.
	- **Transparent Bridge**: The WAF operates without changing the network's topology, analysing traffic passively.
	- **Out-of-Band**: The WAF uses a separate channel for logging and monitoring, without actively interfering with traffic.
2) **Rule-Based Configuration**: WAFs operate based on policies or rules that define acceptable and malicious behaviour. These rules can be custom or preconfigured templates targeting specific vulnerabilities.
3) **Machine learning Integration**: Modern WAFs employ machine learning to detect new, unknown threats based on abnormal behaviour patterns.
4) **Integration Points**:
	- **Network level**: WAFs can be hardware appliances in the data center.
	- **Software level**: Installed as software on web servers.
	- **Cloud-Based**: Managed WAF services, offered by vendors like AWS, Azure, Cloudflare

# Cloudflare WAF
Cloudflare provides a **Cloud-Based WAF** that integrates seamlessly with its **Content Delivery Network (CDN)** and other security features. Here's how it works and is implemented:
1) **DNS-Level Integration**
	- Cloudflare acts as a intermediary between users and the web server by managing DNS records.
	- All traffic to the web application passes through Cloudflare's servers for inspection.
2) **Security Features**
	- **Predefined Rules**: Cloudflare WAF comes with built-in rulesets targeting common vulnerabilities.
	- **Custom Rules**: Users can create custom firewall rules based on specific application needs.
	- **Rate Limiting**: Helps prevent DDoS attacks and abuse by limiting the number of requests from a single IO.
3) **Traffic Monitoring and Analytics**
	-  Cloudflare provides a dashboard for monitoring application traffic, blocked threats, and suspicious activities
	- Threat intelligence updates are automatically applied, keeping the WAF up-to-date against emerging threats.
4) **Scalability and Performance**
	- Being cloud-based, the Cloudflare WAF can handle large amounts of traffic and scales automatically without manual intervention.
	- Traffic is routed through its global network reducing latency and improving application speed
5) **Implementation Steps**
	-  **Set Up Cloudflare Account**: Register the application and point its DNS records to Cloudflare.
	- **Enable WAF**: Turn on the WAF in the Cloudflare Dashboard
	- **Configure Rules**: Apply preconfigured rules or defined custom firewall rules tailored to your application's needs
	- **Monitor Logs**: Use the analytics dashboard to  monitor and refine rules based on attack patterns.

# Azure WAF
Azure WAF is cloud-native managed WAF service that protects Applications hosted in Azure environments. It is integrated with Azure's load balancers and application delivery services.
**Key features**:
- **Protection Against OWASP Top 10 Vulnerabilities**: Azure WAF provides preconfigured rulesets for common vulnerabilities like SQL injection, XSS, etc.
- **Global Threat Intelligence**: Integrated with Microsoft’s global threat detection services for real-time updates.
- **Custom Rules**: Allows users to create rules tailored to specific application needs.
- **Bot Protection**: Detects and blocks malicious bot traffic.
- **Integration**: Works with Azure services such as Application Gateway, Front Door, and CDN.

**How it works**:
1) **Deployment Options**:
	- **Azure Application Gateway**: Azure WAF can be deployed with Azure Application Gateway, a Layer 7 load balancer.
	- **Azure Front Door**: For global load balancing and traffic routing, Azure Waf integration with Front Door.
	- **Azure CDN**: To protect content delivery network traffic
2) **Traffic Inspection**: 
	- Incoming HTTP/S traffic is routed through Azure WAF.
	- The WAF inspects traffic using predefined rulesets and custom policies.
	- Malicious traffic is blocked or logged, while legitimate traffic is forwarded to the application.
3) **Logging and Monitoring**:
	- Logs are sent to Azure Monitor, Log Analytics or Events Hubs for analysis.
	- Alerts can be configured to notify administrators of suspicious activities.

# Amazon Web Services (AWS) WAF
AWS WAF is a managed WAF service that integrated with AWS services to protect application from web exploits. It is highly scalable and customizable.
**Key features**:
- **Integration**: Works with AWS CloudFront (CDN), Application Load Balancer (ALB), and APLI Gateway.
- **Predefined Rule Groups**: Includes AWS-managed rules and third-party rules for common vulnerabilities.
- **Custom rules**: Users can define rate-based rules, block/allow lists, and more.
- **Scalability**: Automatically scaled with traffic demands.
- **Real-Time Monitoring**: Integrated with AWS CloudWatch for monitoring and altering

**How it works**:
1) **Deployment Options**:
	- **Amazon CloudFront**: AWS WAF can be deployed with CloudFront, its global CDN.
	- **Application Load Balancer (ALB)**: Protects web applications behind ALB.
	- **Amazon API Gateway**: Secures API endpoints.
2) **Traffic Inspection**:
	- AWS WAF evaluates incoming HTTP/S requests using rules defined by the user or AWS.
	- Requests are filtered based on rules like IP matching, string matching, SQL injection patterns, etc.
	- Approved traffic is forwarded to the application, while malicious requests are blocked or logged.
3) **Logging and Monitoring**:
	- Logs are stored in Amazon S3 or streamed to CloudWatch for analysis.
	- Real-time metrics provide insights into blocked requests and potential threats.

# WAF BYPASS
Before digging into how we are going to bypass the Web Application Firewall of a web app, we first need to know why it's "bypassable".
### Why are web application firewalls susceptible to bypasses?
They can't just block every request or even every malicious activity, this is mainly because of the complexity of some web traffic. 
**First** just considering the usual formats like:
- .txt (Text)
- .json (JavaScript Object Notation)
- .xml (Extensible Markup Language)
- Multi-part forms
Where WAFs needs to handle all these consistently. 
We can of cause try to attack this handling of things, by obfuscating our payloads in many different ways to make it almost impossible to account for account for every possibility. If the WAF is to wide, we tend to get a lot of false positives, and if it's to narrow, it's easy to bypass.
**Next consider** the performance of the WAF, it needs to inspect every bite of every request, and it's computationally expensive. Therefore many WAFS attempt to optimize their performance by limiting the size or depth of inspections (this can be leveraged later).
**The last thing to consider** before moving on is *inconsistencies in how different technologies process data*, a bit like the old *multiple bit SQL Injection*, since applications and databases interpret input differently, and we can use that difference to evade WAF, some WAFs might decode and interpret our traffic differently to the target application

### First Technique
This is a relatively simple technique, since this relies on the concept of "obfuscation". We can always just encode, double encode, add whitespace, split keywords, etc. to try to bypass WAF with obfuscation. We want to take out payload, and think about the following:
- Is it being blocked?
- If it's being block:
	- Why is it being block?
	- What is happening to the payload
- What part (if any) is being blocked.
	- Try to just manipulate and obfuscate that specific part.
Another alternative could be using **fuzzing**, but that's another talk.

**Step 1**:
A simple payload (this shouldn't go through), to test is the site is bypassable, when it comes to WAF and [[Cross-site Scripting (XSS)]] is:
```html
<img src=x onerror=prompt()>
```
If this doesn't go through, we can take it up a notch.

**Step 2**:
We can try to submit the same payload again, if it doesn't go through, we can check the **network requests** tab, to see if we are getting any form for error messages, or try to intercept the response for an error message.
Let us follow our previously mentioned methodology.
- Why was this blocked? 
- What is happening to our payload?
When working with the previous payload, we start by breaking it down, and see if we are still getting detected.
Modified (does this get detected)
```html
img src=x onerror=prompt()
```
Move on and modify the payload, so that we can **classify the part that's being blocked**.
A neat and handy way is to create a list and then **fuzz** that list, to see if any of them are getting through.
Some common WAFs have a built in detection for **combination of words** so, where *src* and *onerror* is common on that list, here we can use other attributes:
- oNError
- mouseover
- onmouseover
- etc.
And see if this is going through

### Second Technique
By default a lot of WAFs don't check payloads over a specific size, meaning that we can just add a lot of characters in the suffix or prefix of our payload to get over that size. Some of the default sizes of the WAFs are:
- 8 kb <- 10.000 characters
- 16 kb <- 20.000 characters
- 32 kb <- 40.000 characters
- etc <- Multiple the previous character amount by 2
To test for 8kb, we need at least **10.000** characters added on our payload. So our payload becomes (shortened for reading purpose).
```html
<a*10000 img scr=x onerror=prompt()>
```
There are python scripts for this (or create your own for learning purpose) and there is burp suite plugins to automate this.

### Third Technique
This is where we are taking advantage of inconsistent interpretation of data (previously mentioned). This is where we are looking back at the multi bite SQL Injection which is a rare edge case.
This is where we are using both the application and the WAF, where we are using the application to turn something that the **WAF thinks is benign** and the application is going to change our payload to execute.
This technique involves a lot of testing, meaning that it's trial and error.
**Steps**:
- We first start with some input that the application accepts and isn't malicious (e.g. `testing input`)
- We then start to build on that selected input, to see what the filtering looks like (e.g. `testing input<>!@#$£€&/""()^`)
- From the input that we typed, to the input that's processed on the server, there should be a difference, and this is the behaviour that we are going to exploit.
	- Lets say that `""` (quotes) gets stripped by the application, this is a exploit that we can use.
	- We can use the quotes to **split up our payload**, so that it executes on the other side of the WAF.
	- So we have quotes inside the keywords of our payload e.g.:
	```html
		<im"g sr"c=x onerro"r=promp"t()>
	```
	- From this, we can get Cross-Site Scripting.