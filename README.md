# Wireshark Network Analysis Lab

## Overview

This lab demonstrates foundational packet analysis using Wireshark by capturing and analyzing real network traffic. The exercises focus on identifying DNS lookups, examining the TCP three-way handshake, and reconstructing an HTTP conversation using the **Follow TCP Stream** feature.

The purpose of this project is to build practical network troubleshooting skills that are commonly used by Network Engineers, SOC Analysts, Security Engineers, and Incident Responders. By analyzing packet captures instead of relying on assumptions, network issues can be diagnosed quickly and accurately.

---

## Business Problem

Modern organizations rely on network connectivity for nearly every business process including web applications, authentication, email, cloud services, APIs, and file transfers. When connectivity issues, slow performance, or security incidents occur, packet analysis provides the evidence needed to determine the root cause.

This lab demonstrates how Wireshark can be used to:

- Verify DNS name resolution
- Validate successful TCP connections
- Reconstruct application-layer conversations
- Understand how data travels across a network
- Build practical troubleshooting skills used in enterprise environments

---

## Key Concepts

### DNS (Domain Name System)

DNS translates human-readable domain names into IP addresses. Every connection to a website begins with a DNS lookup.

Example:

```
linkedin.com
↓
150.171.22.12
```

---

### TCP Three-Way Handshake

Before data can be exchanged, TCP establishes a reliable connection using three packets:

1. SYN
2. SYN-ACK
3. ACK

A successful handshake confirms both devices are ready to communicate.

---

### Follow TCP Stream

Individual packets only show small pieces of a conversation.

The **Follow TCP Stream** feature reassembles those packets into a complete request and response, allowing analysts to understand the full communication between client and server.

---

## Important Filters

| Filter | Purpose |
|---------|----------|
| `dns` | Displays DNS queries and responses |
| `tcp` | Shows all TCP traffic |
| `tcp.flags.syn == 1` | Displays TCP connection attempts |
| `tcp.flags.reset == 1` | Displays reset (RST) packets |
| `ip.addr == x.x.x.x` | Filters traffic to/from a specific IP |
| `ip.src == x.x.x.x` | Filters traffic from a specific source |
| `tcp.port == 80` | HTTP traffic |
| `tcp.port == 443` | HTTPS traffic |
| `http.request` | Displays HTTP requests |

---

# Captures

## 1. DNS Lookup Capture

### File

`1 - DNS A Record Capture (linkedin.com).pcapng`

### Objective

Capture a DNS query and response. 

Step 1 
- Run Wireshark before typing in anything in CMD

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/d3f73b776ba988fe7c17e497acc7b4365d6851c6/1.%20DNS%20A%20Record%20Capture/0.5%20-%20Wireshark.png)

Step 2 
- in CMD, type in nslookup linkedin.com
- you can see the public IP address of the website.

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/67580eabdd085d1b6fe97b170c38140265a0d61d/1.%20DNS%20A%20Record%20Capture/1.1%20-%20LinkedIn%20(CMD%20-%20Capturing%20a%20DNS%20Lookup).png)

Step 3 
- Apply Filter after capture

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/b6b5d66c96f9bc23c5244805bf93f3f63f0491a7/1.%20DNS%20A%20Record%20Capture/1.2%20-%20DNS%20-%20Apply%20Filter.png)

Step 4 
- Type in DNS for the filter 

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/b6b5d66c96f9bc23c5244805bf93f3f63f0491a7/1.%20DNS%20A%20Record%20Capture/1.3%20-%20DNS%20-%20Filter.png)

Step 5 
- Hit Enter

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/b6b5d66c96f9bc23c5244805bf93f3f63f0491a7/1.%20DNS%20A%20Record%20Capture/1.4%20-%20DNS%20-%20Hiter%20Enter.png)

Step 6 
- DNS Filter Results 

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/b6b5d66c96f9bc23c5244805bf93f3f63f0491a7/1.%20DNS%20A%20Record%20Capture/1.5%20-%20DNS%20-%20Filter%20Results.png)

Step 7 
- DNS Response 
  1. Double click on the packet and go to the path
  2. Domain Name System (response) >> Answers 

![image alt](https://github.com/mtwbusiness909/Wireshark-Lab-MTW/blob/b6b5d66c96f9bc23c5244805bf93f3f63f0491a7/1.%20DNS%20A%20Record%20Capture/1.6%20-%20DNS%20Response.png)






### Analysis

The capture shows the workstation requesting the IPv4 address for **linkedin.com** from a DNS server.

The DNS response returned:

```
150.171.22.12
```

which matched the result shown in Command Prompt.

This demonstrates how DNS resolves hostnames before any web connection can occur.

### What I Learned

- Every web connection begins with DNS.
- DNS traffic is easy to isolate using the `dns` filter.
- Matching DNS queries and responses confirms successful name resolution.

---

## 2. TCP Three-Way Handshake

### File

`2 - TCP Handshake (neverssl.com).pcapng`

### Objective

Observe a successful TCP connection to an HTTP website.

Before capturing, the destination IP was identified using:

```
nslookup neverssl.com
```

Result:

```
34.223.124.45
```

The capture demonstrates:

- SYN
- SYN-ACK
- ACK

These packets establish a reliable TCP session before application data is exchanged.

### What I Learned

- TCP requires a successful handshake before communication begins.
- Missing SYN-ACK packets often indicate connectivity problems.
- Packet flags quickly identify the health of a connection.

---

## 3. Follow TCP Stream

### File

`3 - Following a Full TCP Stream (HTTP & neverssl.com).pcapng`

### Objective

Use **Follow → TCP Stream** to reconstruct an HTTP conversation.

Rather than viewing individual packets separately, Wireshark rebuilt the complete communication between the client and server.

This provided a readable view of:

- HTTP requests
- HTTP responses
- Headers
- Complete application conversation

### What I Learned

- Individual packets only show fragments of communication.
- TCP Stream reconstruction provides context for investigations.
- This feature is valuable during troubleshooting and incident response.

---

# Skills Demonstrated

- Live packet capture using Wireshark
- DNS analysis
- TCP session analysis
- TCP three-way handshake identification
- Packet filtering using display filters
- Network troubleshooting
- Packet inspection
- HTTP traffic analysis
- TCP Stream reconstruction
- Saving and organizing packet captures
- Basic incident response workflow
- Documentation of network analysis findings

---

# Key Takeaways

- DNS resolution is the first step in nearly every network connection.
- Display filters make large packet captures manageable.
- TCP handshakes verify successful communication between hosts.
- Following TCP Streams reconstructs complete network conversations.
- Packet analysis provides evidence-based troubleshooting instead of guesswork.
- Wireshark is an essential tool for Network Engineers, SOC Analysts, Security Engineers, and Incident Responders.

---

# Portfolio Summary

This project demonstrates practical network analysis using Wireshark by capturing DNS traffic, validating TCP session establishment, and reconstructing HTTP conversations. These exercises reinforce core networking concepts while providing hands-on experience with packet inspection, troubleshooting, and protocol analysis that are directly applicable to Network Engineering, Cybersecurity, and SOC Analyst roles.
