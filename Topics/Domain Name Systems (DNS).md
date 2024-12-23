# What is it
The **Domain Name System (DNS)** is a system that translates human-readable domain names (e.g., `www.example.com`) into IP addresses (e.g., `192.0.2.1`) that computers use to identify each other on a network.

# How does it work
1) **DNS Query**: 
	- When you enter a domain name into a browser, the browser sends a DNS query to find the corresponding IP address.
2) **DNS resolver**: 
	- The DNS resolver (usually provide by your ISP (Internet Service Provider) or a public DNS service like Google DNS) checks its cache for the IP address. It it doesn't find it, it queries other DNS servers.
3) **DNS Servers** The query is passed through a hierarchy of DNS servers:
	- **Root DNS Server**: Directs the query to appropriate Top-Level Domain (TLD) server(e.g., `.com`, `.org`)
	- **TLD Server**: Directs the query to the authoritative DNS server for the specific domain.
	- **Authoritative DNS Server**: Returns the IP address of the domain to the resolver.
4) **Response**
	- The DNS resolver sends the IP address back to the browser, which uses it to connect to the web server hosting the requested content.

# Key components of DNS
- **Domain Name**: The human-readable address.
- **IP Address**: The numerical address of a server
- **DNS Records**:
	- **A Record**: Maps a domain to an IPv4 address.
	- **AAAA Record**: Maps a domain to an IPv6 address.
	- **CNAME Record**: Maps one domain name to another.
	- **MX Record**: Specifies the mail server for a domain
	- **TXT Record**: Holds arbitrary text data, often used for verification purposes (e.g., SPF DKIM)
