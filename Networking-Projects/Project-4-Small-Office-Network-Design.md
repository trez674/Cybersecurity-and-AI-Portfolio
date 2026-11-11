# Project 4 — Small Office Network Design

## 1. Project Overview

In this project, I designed a small office network and planned how its devices would communicate.

I also investigated my own network using Windows commands and my router's connected-device list.

**Project type:** Simulated network design with practical Windows investigation.

## 2. Project Objectives

- Understand how routers, switches and end devices connect.
- Create an IP addressing plan for a small office.
- Understand subnet masks and default gateways.
- Investigate network connectivity problems.
- Learn how to identify devices on a real network.

## 3. Office Network Design

The fictional office contains:

- 1 internet connection
- 1 Wi-Fi router
- 1 network switch
- 4 wired desktop computers
- 1 wired network printer
- 1 wireless laptop

### Network Diagram

```text
                 Internet
                    |
                Wi-Fi Router
               192.168.10.1
                 /       \
                /         \
        Network Switch    Laptop
           / | | \        (Wi-Fi)
          /  | |  \
        PC1 PC2 PC3 PC4
          \
        Printer
```

The diagram is a simplified illustration of the intended connections. The printer also connects to the network switch.

The router provides access to other networks, while the switch connects the wired devices within the local office network.

## 4. IP Addressing Plan

**Network:** 192.168.10.0/24

**Subnet mask:** 255.255.255.0

| Device | Planned IP Address | Default Gateway |
|---|---|---|
| Wi-Fi Router (LAN) | 192.168.10.1 | N/A for LAN clients |
| PC 1 | 192.168.10.10 | 192.168.10.1 |
| PC 2 | 192.168.10.11 | 192.168.10.1 |
| PC 3 | 192.168.10.12 | 192.168.10.1 |
| PC 4 | 192.168.10.13 | 192.168.10.1 |
| Printer | 192.168.10.20 | 192.168.10.1 |
| Laptop | 192.168.10.30 | 192.168.10.1 |

These addresses are part of the proposed design, not IP addresses measured on a physical office network.

An unmanaged network switch does not require its own IP address to forward Ethernet traffic.

## 5. How the Network Works

### Local Communication

When PC 1 sends a document to the printer, the traffic can travel through the switch because both devices are on the same local subnet.

### Internet Communication

When PC 1 needs to reach a destination outside the local subnet, it sends the traffic towards its default gateway, 192.168.10.1.

The router then forwards traffic towards the external network.

### Wireless Communication

The laptop connects through Wi-Fi to the router's wireless network.

It can communicate with the wired office devices if the network configuration and security settings permit it.

## 6. Simulated Connectivity Testing

The following results were provided as a troubleshooting exercise. They were not collected from a physical office network.

| Test | Simulated Result |
|---|---|
| PC 1 to printer (192.168.10.20) | Successful |
| PC 1 to router (192.168.10.1) | Successful |
| PC 1 to external IP (8.8.8.8) | Request timed out |

### Troubleshooting Analysis

The successful printer test suggests local communication is working.

The successful router test shows PC 1 can reach its configured gateway.

The failed external ping requires further investigation. Possible explanations include:

- An issue with the router's internet connection.
- Incorrect routing or upstream connectivity.
- A firewall blocking ICMP traffic.
- The external destination not responding to ping requests.

A failed ping does not automatically prove that the internet connection is down.

**Next diagnostic action:** Check the router's internet status and test another external destination or service.

## 7. Practical Windows Network Investigation

I carried out a separate investigation on my own Windows computer.

### Command 1: ipconfig

I ran:

```cmd
ipconfig
```

I successfully located my computer's default gateway.

I learned that the default gateway is normally the router used to reach destinations outside the local network.

### Command 2: arp -a

I ran:

```cmd
arp -a
```

The output contained several IP and MAC address mappings.

I learned that ARP helps Windows associate IPv4 addresses with link-layer MAC addresses on the local network.

The ARP table does not necessarily contain every connected device, and some entries represent special network addresses rather than individual devices.

### Router Investigation

I entered my default gateway address into a web browser and reached my router's management interface.

I located the connected-device list.

The router displayed MAC addresses, but I could not open individual device details to confirm their IP addresses.

This investigation demonstrated that different routers provide different levels of device information.

I did not modify any router settings.

## 8. Skills Developed

Through this project, I practised:

- Small office network design
- IP address planning
- Subnet and default gateway concepts
- Router and switch roles
- Basic network troubleshooting
- Windows command-line investigation
- Understanding IP and MAC addresses
- Using a router's connected-device interface
- Documenting technical findings

## 9. Conclusion

This project helped me understand how a small office network could be designed and how its devices would communicate.

I also gained practical experience investigating my own network using Windows commands and my router's management interface.

The office network was a simulated design, while the Windows commands and router investigation were completed on a real network.

My next learning goal is to build on these networking fundamentals by studying cybersecurity threats, vulnerabilities, access control and network security.
