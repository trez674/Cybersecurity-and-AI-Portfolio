# Project 1: Basic Network Connectivity Investigation

## Objective
To investigate my Windows PC's network configuration and test its ability to communicate with an external server.

## Tools Used
- Windows Command Prompt
- `ipconfig`
- `ping`
- `nslookup` (next test)

## Test 1: Network Configuration
**Command:** `ipconfig`

I identified the following network information:
- IPv4 address
- Subnet mask
- Default gateway

**What I learned:** These settings help my PC communicate with devices on my local network and other networks.

## Test 2: Network Connectivity
**Command:** `ping 1.1.1.1`

**Results:**
- Packets sent: 4
- Packets received: 4
- Packet loss: 0%
- Status: Successful

**What I learned:** My PC successfully communicated with an external IP address using ICMP.

## Test 3: DNS Resolution
**Command:** `nslookup google.com`

**Result:** Successful. The command returned IP addresses for google.com.

## Conclusion
My initial network connectivity test was successful, with no packet loss. This project helped me practise basic Windows networking commands and understand how network connectivity is tested.

## Next Steps
Complete the DNS test and learn more about troubleshooting network problems.
