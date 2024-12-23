# What is it
A **Content Delivery Network (CDN)** is a network of servers distributed across multiple geographic locations to deliver web content and resources (like images, videos, JavaScript files, and HTML) to users more quickly and efficiently

# How it works
1) **Content Replication**:
	- The CDN replicated and caches content from your main server (origin server) to serves in multiple locations (edge servers) worldwide
2) **Content Delivery**:
	- When a users requests content (e.g., visiting a website), the CDN routes the requests to the nearest edge server rather than the origin server. This minimizes the physical distance the data has to travel.
3) **Caching**:
	- Static resources like images, stylesheets, and scripts are cached on edge servers. Dynamic content can also be optimized using CDNs.
4) **Load Balancing**:
	- CDN distribute traffic across servers, preventing any single server from becoming overwhelmed.

# Benefits
**Reduced Latency**: By serving content from the nearest edge server, users experience faster loading times
**Improved Performance**: CDNs optimizes resource delivery, reducing bandwidth usage and speeding up downloads.
**Scalability**: CDNs handle large traffic volumes efficiently, especially during spikes (e.g., product launches, streaming events.).
**Enhanced Security**: Many CDNs include protection against DDoS attacks and provide encrypted HTTPS delivery.
