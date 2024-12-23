The **OSI Model (Open Systems Interconnection Model)** is a conceptual framework that standardizes how data is transmitted over a network. It divides the communication process into **7 layers**, each with specific responsibilities. This layered approach makes it easier to understand, implement, and troubleshoot network communication.

| Layer | Name         | Description                                                                      | Example Protocols/<br>Technologies   |
| ----- | ------------ | -------------------------------------------------------------------------------- | ------------------------------------ |
| 7     | Application  | Interface for the user to interact with the network (services and applications). | HTTP, FTP, SMTP, DNS                 |
| 6     | Presentation | Formats and encrypts data for the application layer.                             | JPEG, MP4, SSL/TLS                   |
| 5     | Session      | Manages connection and sessions between devices.                                 | NetBIOS, RPC                         |
| 4     | Transport    | Ensures reliable delivery of data (end-to-end communication).                    | TCP, UDP                             |
| 3     | Network      | Handles logical addressing and routing of packets between devices.               | IP, ICMP, ARP, RIP                   |
| 2     | Data Link    | Transfers data frames between two devices on the same network                    | Ethernet, Wi-Fi(802.11), MAC         |
| 1     | Physical     | Transmits raw bitstreams over a physical medium (cables, wireless signals).      | Ethernet cables, Fiber optics, Wi-Fi |

# Detailed Breakdown of Each Layer
1) Physical Layer
	- **Purpose**: Transmits raw bits (0s and 1s) over the physical medium (e.g., cables, radio waves)
	- **Key Functions**:
		- Defines hardware specifications (e.g., cables, connectors, voltage levels).
		- Handles the physical connection between devices.
	- **Examples**: Ethernet cables, Fiber optics, radio waves, hubs.
2) Data Link Layer
	- **Purpose**: Ensures reliable data transfer over the physical link by organizing raw bits into **frames**
	- **Key Functions**
		- Error detection and correction (e.g., Cyclic Redundancy Check, CRC).
		- Media Access Control (MAC) for addressing devices.
		- Manages flow control.
	- **Examples**:
		- Protocols: Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11).
		- Hardware: Switches, Network Interface Cards (NICs).
3) Network Layer 
	- **Purpose**: Handles logical addressing and routing of data packets across multiple networks
	- **Key Functions**
		- Logical addressing (e.g., IP addresses).
		- Routing packets through routers.
		- Fragmentation and reassembly of packets.
	- **Examples**:
		- Protocols: Internet Protocol (IP), Internet Control Message Protocol (ICMP), Address Resolution Protocol (ARP).
		- Devices: Routers
4) Transport layer:
	- **Purpose**: Ensures reliable data delivery between end systems (hosts) by managing data flow and error recovery.
	- **Key Functions**
		- Segmentation of data into smaller chunks.
		- Reliable delivery (acknowledgments, retransmissions).
		- Flow control to prevent overwhelming receivers.
	- **Examples**:
		- Protocols: Transmission Control Protocol (TCP) for reliable communication, User Datagram Protocol (UDP) for faster, connectionless communication.
5) Session Layer 
	- **Purpose**: Manages sessions or connections between applications.
	- **Key Functions**:
		- Established, maintains, and terminates communication sessions.
		- Synchronization (e.g., checkpoints in a file transfer).
	- **Examples**:
		- Protocols: Remote Procedure Call (RPC), Network Basic Input/Output System (NetBIOS).
6) Presentation Layer
	-  **Purpose**: Translates data between the application and the network (data formatting and encryption).
	- **Key functions**
		- Data encoding/decoding (e.g., converting text to ASCII or EBCDIC).
		- Data compression.
		- Encryption and decryption for security.
	- **Examples**
		- Formats: JPEG, PNG, FIG, MP4
		- Encryption: SSL/TLS
7) Application Layer
	- **Purpose**: Provides network services directly to the user's application.
	- **Key Functions**
		- Network resource sharing (e.g., file transfer, email).
		- User interface for network communication.
	- **Examples**
		- Protocols: Hypertext Transfer Protocol (HTTP), File Transfer Protocol (FTP), Domain Name System (DNS), Simple Mail Transfer Protocol (SMTP)

# How it works
When you send an email or access a website:
1) **Application Layer**: A web browser (application) send a request via HTTP.
2) **Presentation Layer**: Data is formatted and encrypted (e.g., with SSL/TLS).
3) **Session Layer**: A session is established between your device and the server.
4) **Transport Layer**: Data is segmented into packets, and TCP ensures delivery.
5) **Network Layer**: Packets are assigned IP addresses and routed to the destination.
6) **Data Link Layer**: Framed are created with MAC addresses to identify devices on the same network.
7) **Physical Layer**: Frames are converted to electrical signals and transmitted.

When the server responds, the process happens in reverse.