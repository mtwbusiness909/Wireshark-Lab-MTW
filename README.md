# Network Analysis (Wireshark)

> **Tools Used:** Wireshark, Windows Command Prompt (CMD)

---

# Overview

This lab demonstrates how to capture and analyze network traffic using Wireshark. The exercise focuses on understanding common networking protocols, including DNS, TCP, HTTP, and HTTPS. By capturing live traffic and applying display filters, we can observe how devices communicate across a network and gain hands-on experience with network troubleshooting and protocol analysis.

**Screenshot:**
- Wireshark capturing live network traffic.

---

# Business Problem

Organizations depend on reliable network communication for websites, cloud services, email, and business applications. When connectivity issues occur, network administrators and cybersecurity professionals use packet analyzers like Wireshark to identify the root cause of problems. Analyzing network traffic helps troubleshoot DNS failures, connection issues, slow performance, and potential security incidents.

---

# Definitions of Key Concepts

## Definitions of Key Concepts

### Packets - Packets are small pieces of data that travel across a network between devices.

### Network Protocols - Network protocols are rules that allow devices to communicate with each other over a network.

### TCP (Three-Way Handshake) - The TCP three-way handshake is a process that establishes a reliable connection between a client and a server before data is sent.

### DNS - DNS (Domain Name System) translates domain names, like `google.com`, into IP addresses that computers can use.

### HTTP vs HTTPS - HTTP is used to transfer web data, while HTTPS encrypts the data to provide a secure connection.

---

# Essential Display Filters

| Filter | Description |
|---------|-------------|
| `dns` | Displays only DNS traffic |
| `tcp` | Displays only TCP packets |
| `http` | Displays HTTP traffic |
| `tls` | Displays encrypted HTTPS/TLS traffic |
| `ip.addr == x.x.x.x` | Shows traffic to or from a specific IP address |
| `tcp.port == 80` | Filters HTTP traffic |
| `tcp.port == 443` | Filters HTTPS traffic |

**Screenshot:**
- Wireshark using the `dns` and `tcp` display filters.

---

# Captures

## First Capture (DNS Lookup)

### What is a DNS Lookup?

A DNS lookup is the process of converting a domain name into an IP address. When a user visits a website, the computer sends a DNS query to a DNS server requesting the IP address associated with the domain. The DNS server responds with the appropriate IP address, allowing the browser to establish a connection.

### Steps

1. Start a Wireshark capture.
2. Apply the display filter:
   ```
   dns
   ```
3. Open Command Prompt.
4. Run:
   ```
   nslookup google.com
   ```
5. Observe the DNS Query and DNS Response packets.

**Screenshots:**

- Command Prompt showing the `nslookup` command.
- DNS Query packet.
- DNS Response packet.
- Packet Details showing the Answer section.

---

## Second Capture (TCP Handshake)

### What is a TCP Handshake?

The TCP three-way handshake establishes a reliable connection before any data is exchanged.

Sequence:

```
Client                 Server

SYN ------------------>

     <------------- SYN, ACK

ACK ------------------>
```

### Steps

1. Start a new capture.
2. Open a website or connect to a server.
3. Apply the filter:
   ```
   tcp
   ```
4. Locate the SYN, SYN-ACK, and ACK packets.

**Screenshots:**

- Packet list showing the three handshake packets.
- Packet Details highlighting the TCP Flags.
- Expanded TCP header showing the SYN and ACK flags.

---

## Third Capture (Stream Follow)

### What is Stream Follow?

Follow TCP Stream reconstructs an entire conversation between two hosts by combining multiple TCP packets into readable application-layer data.

This feature helps analysts:

- View complete HTTP requests and responses.
- Analyze client/server conversations.
- Troubleshoot application communication.

### Steps

1. Select a TCP packet.
2. Right-click the packet.
3. Select:
   ```
   Follow
   →
   TCP Stream
   ```
4. Review the reconstructed conversation.

**Screenshots:**

- Right-click menu showing **Follow → TCP Stream**.
- Follow TCP Stream window.
- HTTP request/response (if available).

---

# Common Troubleshooting

| Problem | Solution |
|----------|----------|
| No packets captured | Verify the correct network adapter is selected. |
| No DNS packets | Generate traffic using `nslookup`. |
| No HTTP packets | Most websites use HTTPS; use the `tls` filter instead. |
| Too many packets | Apply display filters such as `dns`, `tcp`, or `http`. |
| TCP handshake not visible | Start capturing before opening the website or application. |

---

# Skills Demonstrated

- Network packet capture using Wireshark
- Network traffic analysis
- DNS request and response analysis
- TCP three-way handshake analysis
- Applying Wireshark display filters
- Following TCP streams
- Protocol identification
- Basic network troubleshooting
- Packet inspection and analysis

---

# Key Takeaways

- Wireshark captures and analyzes live network traffic.
- DNS resolves domain names into IP addresses before communication begins.
- TCP establishes reliable connections using the three-way handshake.
- Display filters simplify packet analysis by isolating specific protocols.
- Following TCP streams reconstructs complete conversations between hosts.
- Packet analysis is an essential skill for network administrators, IT professionals, and cybersecurity analysts.

---

# Screenshot Checklist

- ✅ Wireshark capturing live traffic
- ✅ Packet Details pane expanded
- ✅ Command Prompt showing `nslookup google.com`
- ✅ DNS Query packet
- ✅ DNS Response packet
- ✅ `dns` display filter
- ✅ TCP SYN packet
- ✅ TCP SYN-ACK packet
- ✅ TCP ACK packet
- ✅ TCP Flags expanded
- ✅ `tcp` display filter
- ✅ Right-click menu showing **Follow → TCP Stream**
- ✅ Follow TCP Stream window
- ✅ HTTP request/response or TLS stream (optional)
