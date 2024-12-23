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
	