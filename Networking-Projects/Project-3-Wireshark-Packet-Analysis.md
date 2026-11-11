# Project 3: Wireshark Network Packet Analysis

## Project Overview

This project involved capturing and analysing live network traffic using Wireshark on a Windows computer.

The aim was to understand how common network protocols work, investigate DNS queries and responses, and develop practical network troubleshooting skills.

## Tools Used

- Windows computer
- Wireshark
- Windows Command Prompt
- Wi-Fi network connection
- Cloudflare public DNS server (`1.1.1.1`)

## 1. Capturing Network Traffic

I opened Wireshark and selected my active Wi-Fi network interface.

I started a live packet capture and observed packets appearing continuously, even when I was not actively browsing the internet.

I learned that background services, applications and operating system processes can generate network traffic automatically.

## 2. Identifying Network Protocols

I examined the Protocol column in Wireshark and identified the following protocols:

| Protocol | Purpose |
|---|---|
| TCP | Provides reliable, ordered data transport |
| UDP | Provides connectionless datagram transport |
| DNS | Resolves domain names and provides DNS records |
| TLS | Protects communications using encryption |

This helped me understand that different protocols perform different roles in network communication.

## 3. Generating DNS Traffic

I started a new packet capture in Wireshark.

I opened Windows Command Prompt and entered:

`nslookup example.com 1.1.1.1`

I then stopped the packet capture and applied the Wireshark display filter:

`dns`

This allowed me to locate DNS queries and responses in the captured network traffic.

## 4. Investigating a DNS Query

I selected a DNS query packet and expanded the Domain Name System section in the Packet Details panel.

### Observed Query Details

| Field | Result |
|---|---|
| Transaction ID | `0x0002` |
| Requested name | `example.com.Home` |
| Query type | `A` |
| DNS class | `IN` |
| Number of questions | `1` |
| Answer records in query | `0` |

The A record type indicates a request for an IPv4 address.

I noticed that the requested name contained `.Home` after `example.com`.

This may have been caused by a DNS search suffix configured on my computer or network, although I have not confirmed the exact cause.

## 5. Investigating the DNS Response

Wireshark displayed a link labelled:

`[Response In: 203]`

I followed this link to locate the matching DNS response.

### Observed Response Details

| Field | Result |
|---|---|
| Response packet number | `203` |
| Transaction ID | `0x0002` |
| Response flags | `0x8183` |
| Response status | `No such name` (NXDOMAIN) |

The DNS server reported that the requested name could not be found.

This result applied to `example.com.Home`, not necessarily to `example.com`.

The matching transaction ID helped confirm the relationship between the query and response.

## 6. Cybersecurity Relevance

Wireshark is useful for network troubleshooting and cybersecurity investigations.

Packet analysis can help identify:

- DNS resolution problems
- Unexpected network connections
- Unusual traffic patterns
- Communication between devices
- Potential indicators requiring further security investigation

However, unusual traffic or a failed DNS lookup does not automatically indicate malicious activity.

## 7. Skills Developed

Through this project, I learned how to:

- Capture live network traffic in Wireshark
- Select and inspect individual packets
- Identify TCP, UDP, DNS and TLS traffic
- Apply the `dns` display filter
- Generate DNS traffic using `nslookup`
- Expand protocol details in Wireshark
- Identify a DNS A-record query
- Match a DNS query to its response
- Interpret an NXDOMAIN response
- Document technical findings accurately

## 8. Conclusion

I successfully captured and analysed network traffic using Wireshark.

I identified several common network protocols and performed a detailed DNS investigation.

During the investigation, I observed an A-record query for `example.com.Home` and followed it to its matching response in packet 203.

The response returned NXDOMAIN, indicating that the requested name could not be found.

This project improved my understanding of DNS, network protocols and practical packet analysis.

## Next Steps

- Investigate why `.Home` was appended to the queried domain
- Examine successful DNS responses and their answer records
- Investigate TCP connection establishment and the three-way handshake
- Continue developing practical network troubleshooting skills
