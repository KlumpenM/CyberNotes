When it comes to scanning, or active scanning we can use a sea of different tools. One of the better tools for active scanning (other than [[Burp Suite]]) is [[Nikto]].


# Nikto
Nikto is one of my personal go to tools (when we are talking web pen testing), when it comes to actively scanning a website. 
The most basic command, that we are using here is:
```
nikto -h <website>
```
- More advanced patterns, can be seen in this: [[Nikto]].
We are not getting the most informational out of this. This is not a tool that is that used when it comes to bug bounty. 
But what is then nice about this, since we are not using it for bug bounty?
Nikto is a vulnerability scanner, it well tell us information about the target:
- IP address
- SSL certification
	- Sometimes we are finding wildcard certification **bad**
- Header information
	- Anti-headers is missing
- If [[WAF - Web Application Firewall]] is present
It mostly just tells us if some of the back lying structure is vulnerable.


# Nmap (SSL)
That that (if we were lucky) Nikto will have given us the [[SSL certification]]. But what if we want to look at the cyphers that the website/server is using.
This is what we can use Nmap for (and much more look here: [[Nmap]])
We are running the command:
```
nmap -p 443 --script=ssl-enum-ciphers <ip-address>
```
Here we are looking at the following: (from the flags)
- Port: 443
	- Since we are working with a website that enforces HTTPS (could potentially not enforce it, then try port 80 or a combination)
- Script: SSL-Enum-Ciphers
	- This script repeatedly initiates SSLv3/TLS connections, each time trying a new cipher or compressor while recording whether a host accepts or rejects it. The end result is a list of all the ciphersuites and compressors that a server accepts.
	- It gives it a grade between A-F (A best)
	- More about it [here](https://nmap.org/nsedoc/scripts/ssl-enum-ciphers.html) (recommended).
From this command we are looking at the TLS ciphers that they are using, and looking for low grades (around E-F). 
We scroll to the bottom of the output, to see the least strength cipher that they are using.
- If we get a grade around E-F, we can try to exploit the ciphers, it's very hard and many people don't do it in their lifetime. *But it's left for the reader as an exercise*.
But it's great to report back as a vulnerability assessment.

# Nmap (Web Server Fingerprinting)
To look at the [[Web Server Fingerprinting]], we can also use Nmap, here we are using the command:
```
nmap -p80,443 -A -T4 <ip-address>
```
Here we are looking at the following: (from the flags)
- Ports: 80 and 443
	- Now we are both looking at the HTTP and the HTTPS version.
- A flag:
	- This is also called the "Aggressive Detection Mode " and it runs several operations at once:
		- -O: OS detection
		- -sV: What version of services are running on the target host
- T flag:
	- This is a flag with a value between 0 and 5. These timing templates affect many variables, offering a simple way to adjust overall Nmap speed from very slow (`-T0`) to extremely aggressive ( `-T5`). A timing template may be combined with the more granular options describe below, and the most granular option takes precedence.
In the output we get a lot of information, some of it is useful, while something might not be useful.
Look at [[Nmap]] for more information.
