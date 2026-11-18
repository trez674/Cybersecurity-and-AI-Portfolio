# Project 5 — Network Scanning and Device Discovery

## Project Overview

This project investigates a Windows computer's local network configuration, router connectivity, ARP cache, and active network connections using built-in Windows PowerShell commands.

The project also includes an investigation of a running Windows process to understand its role and assess whether its executable is consistent with legitimate Microsoft software.

## Objectives

- Identify local network configuration details.
- Test connectivity to the default gateway.
- Examine devices recorded in the ARP cache.
- Identify listening and established network connections.
- Associate a process ID (PID) with a running process.
- Investigate a Windows service, executable path, and digital signature.
- Document findings and limitations accurately.

## Tools and Environment

- Operating system: Windows
- Command-line environment: PowerShell
- Tools: `ipconfig`, `ping`, `arp`, `netstat`, `Get-Process`, `Get-Service`, `sc.exe`, `Get-CimInstance`, and `Get-AuthenticodeSignature`

## Investigation Steps

### Step 1 — Identify Network Configuration

**Command:**

```powershell
ipconfig /all
```

Used this command to inspect the computer's network configuration, including its IPv4 address, subnet mask, and default gateway.

**Finding:** Identified the local network settings and the router's gateway address.

### Step 2 — Test Router Connectivity

**Command:**

```powershell
ping <default-gateway-IP>
```

Replaced the placeholder with the default gateway address identified in Step 1.

**Finding:** Received successful replies from the default gateway, indicating that the gateway responded to the connectivity test.

### Step 3 — Examine the ARP Cache

**Command:**

```powershell
arp -a
```

Examined the ARP cache, including internet addresses, physical (MAC) addresses, and entry types.

**Finding:** Located the default gateway's IP address in the ARP cache and observed its associated physical address.

**Limitation:** The ARP cache only contains entries known to the computer; it is not a complete inventory of all devices on the network.

### Step 4 — Investigate Network Connections

**Command:**

```powershell
netstat -ano
```

Examined network connections and their associated process IDs.

**Finding:** Observed TCP connections in `ESTABLISHED` and `LISTENING` states.

Selected a listening connection associated with PID `3428` for further investigation.

### Step 5 — Identify the Process

**Command:**

```powershell
Get-Process -Id 3428
```

**Finding:** Identified the process name as `vmms`, which is commonly associated with Microsoft Hyper-V Virtual Machine Management.

The PID was observed during this investigation and may change when the process restarts.

### Step 6 — Examine Process and Service Information

**Commands:**

```powershell
Get-CimInstance Win32_Process -Filter "ProcessId = 3428" | Select-Object Name, ExecutablePath
```

```powershell
Get-Service -Name vmms
```

The process query returned `vmms.exe`, but the `ExecutablePath` field was blank. This did not establish the executable's location.

The service query confirmed that the `vmms` service was registered and running.

### Step 7 — Verify the Service Configuration

**Command:**

```powershell
sc.exe qc vmms
```

**Finding:** The service configuration showed the expected executable path:

```text
C:\Windows\System32\vmms.exe
```

### Step 8 — Verify the Digital Signature and Publisher

**Commands:**

```powershell
Get-AuthenticodeSignature "C:\Windows\System32\vmms.exe"
```

```powershell
(Get-AuthenticodeSignature "C:\Windows\System32\vmms.exe").SignerCertificate.Subject
```

**Findings:**

- Digital signature status: `Valid`
- Signing certificate subject: Identified Microsoft as the publisher

These results support the assessment that the configured executable is consistent with legitimate Microsoft software.

## Security Analysis

The investigation demonstrated how an analyst can start with an observed listening network connection and investigate the associated Windows process.

The `vmms` process was associated with a running Windows service, a configured executable path in the Windows system directory, and a file with a valid digital signature identifying Microsoft.

No evidence of malicious activity was identified during these checks.

However, a valid digital signature does not guarantee that all activity involving a program is safe. The investigation also did not independently establish that the live process was executing the exact file whose signature was checked.

## Limitations

- This was a local network configuration and connection investigation, not a comprehensive active network scan.
- The ARP cache does not list every device connected to a network.
- No vulnerability scan, penetration test, packet capture, or malware analysis was performed.
- The investigation did not verify every network connection or process.
- The findings reflect the system state observed during the exercise.

## Conclusion

This project provided hands-on experience with Windows network discovery, connectivity testing, network connection analysis, process identification, Windows service inspection, and executable signature verification.

It demonstrated a basic cybersecurity investigation workflow: observe a network connection, identify the associated process, examine its service configuration, verify supporting evidence, and document a conclusion without overstating the results.

## Skills Demonstrated

- Windows PowerShell fundamentals
- Local network configuration analysis
- Gateway connectivity testing
- ARP cache inspection
- TCP connection and PID analysis
- Windows process and service investigation
- Digital signature verification
- Evidence-based security reporting
