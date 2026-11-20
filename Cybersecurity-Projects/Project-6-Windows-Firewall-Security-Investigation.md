# Project 6 — Windows Firewall Security Investigation

## Case 001: Investigation of a Public Network Firewall Rule

### 1. Executive Summary

This project documents a hands-on investigation of Windows Defender Firewall settings on a Windows computer.

The objective was to identify potentially unnecessary inbound network permissions, investigate a printing-related firewall rule, and assess whether the available evidence indicated a security concern.

The investigation identified an enabled inbound firewall rule named **Wi-Fi Direct Spooler Use (In)** that applies to the **Public** network profile.

The rule allows traffic associated with the Windows Print Spooler executable, `spoolsv.exe`. The executable had a valid digital signature identifying Microsoft as the signer.

**Final assessment:** The rule may represent unnecessary inbound network permission if Wi-Fi Direct printing is not required. However, no malicious activity, successful unauthorised access, or exploitable vulnerability was confirmed.

**Recommendation:** Review the business need for Wi-Fi Direct printing before making any firewall changes.

---

## 2. Investigation Scenario

**Role:** Junior SOC Analyst  
**Case ID:** 001  
**Investigation Type:** Windows Firewall Configuration Review  
**Environment:** Windows computer using PowerShell  
**Approach:** Read-only security investigation

### Scenario

A supervisor requested an investigation into the computer's firewall configuration to determine whether any enabled rules could permit unnecessary incoming network connections.

The analyst was instructed to collect evidence, identify potentially risky permissions, and recommend appropriate next steps without modifying system settings.

### Objectives

- Verify that Windows Firewall is enabled.
- Identify the active network profile.
- Examine effective inbound and outbound firewall behaviour.
- Review enabled inbound Allow rules.
- Investigate a specific printing-related firewall rule.
- Verify the associated executable's digital signature.
- Examine relevant Windows services and listening TCP ports.
- Document findings and recommendations.

---

## 3. Tools Used

- Windows PowerShell
- Windows Defender Firewall PowerShell cmdlets
- Windows service management cmdlets
- Authenticode digital signature verification
- Windows printer management cmdlets
- TCP connection inspection

All investigation commands were read-only.

---

## 4. Investigation and Evidence

### Step 1 — Verify Windows Firewall Profiles

**Command:**

```powershell
Get-NetFirewallProfile
```

**Finding:**

All three firewall profiles were enabled:

| Profile | Enabled |
|---|---|
| Domain | True |
| Private | True |
| Public | True |

**Interpretation:**

Windows reported that the firewall was enabled for all three profiles.

This did not establish that every network connection was blocked or that all firewall rules were appropriately configured.

### Step 2 — Examine Firewall Defaults

**Commands:**

```powershell
Get-NetFirewallProfile | Select-Object Name, DefaultInboundAction, DefaultOutboundAction
```

```powershell
Get-NetFirewallProfile -Name Private | Select-Object Name, Enabled, DefaultInboundAction, DefaultOutboundAction
```

**Finding:**

The Private profile displayed `NotConfigured` for its inbound and outbound default actions.

The Public profile also initially displayed `NotConfigured` for its default inbound action.

**Interpretation:**

`NotConfigured` did not mean the firewall was disabled or that all incoming traffic was allowed.

Additional checks were required to examine the effective firewall policy.

### Step 3 — Identify the Active Network Profile

**Command:**

```powershell
Get-NetConnectionProfile
```

**Finding:**

```text
NetworkCategory : Public
```

**Interpretation:**

Windows classified the active network connection as Public.

The Public firewall profile was therefore the main focus of the investigation.

### Step 4 — Examine Effective Public Firewall Policy

**Commands:**

```powershell
Get-NetFirewallProfile -Name Public -PolicyStore ActiveStore | Select-Object Name, Enabled, DefaultInboundAction
```

```powershell
Get-NetFirewallProfile -Name Public -PolicyStore ActiveStore | Select-Object Name, DefaultOutboundAction
```

**Findings:**

| Setting | Result |
|---|---|
| Public firewall enabled | True |
| Effective default inbound action | Block |
| Effective default outbound action | Allow |

**Interpretation:**

The active Public firewall policy blocked incoming traffic by default unless an applicable rule permitted it.

Outgoing traffic was allowed by default, subject to applicable rules and other security controls.

### Step 5 — Review Firewall Rules

**Command to count enabled outbound Block rules:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -Enabled True -Direction Outbound -Action Block | Measure-Object
```

**Result:**

```text
Count : 0
```

No enabled outbound Block rules were found by this query.

**Command to count enabled inbound Allow rules:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -Enabled True -Direction Inbound -Action Allow | Measure-Object
```

**Result:**

```text
Count : 176
```

The active policy contained 176 enabled inbound Allow rules across firewall profiles.

### Step 6 — Identify Rules Including the Public Profile

An initial filtering attempt using the following expression produced an error:

```powershell
$_.Profile -band 4
```

**Error:**

```text
Where-Object : Specified cast is not valid.
```

The investigation continued using a text-based profile filter:

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -Enabled True -Direction Inbound -Action Allow | Where-Object { $_.Profile.ToString() -match 'Public|Any' } | Measure-Object
```

**Result:**

```text
Count : 116
```

This query found 116 enabled inbound Allow rules whose displayed profile values matched `Public` or `Any`.

**Limitation:** This was a count based on the selected filtering method, not proof that 116 connections or ports were exposed.

### Step 7 — Review Selected Public Firewall Rules

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -Enabled True -Direction Inbound -Action Allow | Where-Object { $_.Profile.ToString() -match 'Public|Any' } | Select-Object -First 5 DisplayName, Profile
```

**Results:**

| Rule | Profile |
|---|---|
| Wi-Fi Direct Spooler Use (In) | Public |
| Core Networking - IPv6 (IPv6-In) | Any |
| Delivery Optimization (UDP-In) | Any |
| Core Networking - Router Advertisement (ICMPv6-In) | Any |
| Core Networking - Destination Unreachable Fragmentation Needed (ICMPv4-In) | Any |

The **Wi-Fi Direct Spooler Use (In)** rule was selected for closer investigation because it was printing-related and applied to the Public profile.

### Step 8 — Examine the Printing Firewall Rule

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -DisplayName "Wi-Fi Direct Spooler Use (In)" | Format-List DisplayName, Enabled, Direction, Action, Profile
```

**Results:**

```text
DisplayName : Wi-Fi Direct Spooler Use (In)
Enabled     : True
Direction   : Inbound
Action      : Allow
Profile     : Public
```

**Interpretation:**

The rule was enabled and permitted matching inbound traffic on Public networks.

This was not evidence that the computer had been accessed.

### Step 9 — Examine Protocol and Port Restrictions

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -DisplayName "Wi-Fi Direct Spooler Use (In)" | Get-NetFirewallPortFilter | Format-List Protocol, LocalPort, RemotePort
```

**Reported results:**

```text
Protocol  : Any
LocalPort : Any
```

**Interpretation:**

The inspected rule did not specify a particular protocol or local port.

This did not mean that every port was open, because additional firewall conditions and network controls could still restrict traffic.

### Step 10 — Identify the Associated Application

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -DisplayName "Wi-Fi Direct Spooler Use (In)" | Get-NetFirewallApplicationFilter | Format-List Program
```

**Result:**

```text
Program : C:\WINDOWS\system32\spoolsv.exe
```

**Interpretation:**

The rule referenced the standard Windows Print Spooler executable path.

### Step 11 — Verify the Digital Signature

**Commands:**

```powershell
Get-AuthenticodeSignature "C:\Windows\System32\spoolsv.exe" | Select-Object Status
```

```powershell
(Get-AuthenticodeSignature "C:\Windows\System32\spoolsv.exe").SignerCertificate.Subject
```

**Findings:**

- Signature status: `Valid`
- Certificate subject: Identified Microsoft

**Interpretation:**

The file's signature passed verification and its signing certificate identified Microsoft.

These findings were consistent with legitimate Windows software but did not guarantee that the service or firewall permission could never be misused.

### Step 12 — Check the Print Spooler Service

**Command:**

```powershell
Get-Service -Name Spooler
```

**Result:**

```text
Status : Running
```

**Interpretation:**

The Windows Print Spooler service was running during the investigation.

This did not establish that a print job was active or that a remote connection had occurred.

### Step 13 — Review Configured Printers

**Command:**

```powershell
Get-Printer | Select-Object Name, Type, PortName
```

**Results:**

| Name | Type | Port |
|---|---|---|
| Fax | Local | SHRFAX: |
| Microsoft Print to PDF | Local | PORTPROMPT: |
| Microsoft XPS Document Writer | Local | PORTPROMPT: |
| OneNote (Desktop) | Local | nul: |

**Interpretation:**

The listed printers were local entries, and no obvious physical network printer was identified.

This raised a reasonable question about whether the Public-profile printing permission was necessary.

However, the absence of a network printer in this output did not prove that Wi-Fi Direct printing functionality was unused.

### Step 14 — Check Remote Address Restrictions

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -DisplayName "Wi-Fi Direct Spooler Use (In)" | Get-NetFirewallAddressFilter | Format-List RemoteAddress
```

**Result:**

```text
RemoteAddress : Any
```

**Interpretation:**

The rule did not restrict permitted traffic to specific remote IP addresses.

Other firewall conditions could still apply.

### Step 15 — Check Network Interface Restrictions

**Command:**

```powershell
Get-NetFirewallRule -PolicyStore ActiveStore -DisplayName "Wi-Fi Direct Spooler Use (In)" | Get-NetFirewallInterfaceTypeFilter | Format-List InterfaceType
```

**Result:**

```text
InterfaceType : Any
```

**Interpretation:**

The rule did not restrict traffic to a particular network interface type.

### Step 16 — Inspect Listening TCP Ports

**Command:**

```powershell
Get-NetTCPConnection -State Listen | Select-Object LocalAddress, LocalPort, OwningProcess
```

**Selected results:**

| Local address | Port | PID |
|---|---|---|
| :: | 135 | 1772 |
| :: | 445 | 4 |
| :: | 2179 | 3428 |
| 0.0.0.0 | 5040 | 10648 |
| 192.168.0.30 | 139 | 4 |
| :: | 49664–49669 | Various |

The output also included additional IPv4 and IPv6 listening endpoints.

**Interpretation:**

Several TCP ports were listening for possible connections.

However, the process IDs were not matched to the Print Spooler process during this check.

Therefore, the investigation did not establish whether the Print Spooler was listening on a TCP port.

UDP listeners were not examined.

Listening ports also did not establish external accessibility or unauthorised access.

---

## 5. Security Finding

### Finding 001 — Potentially Unnecessary Public Inbound Firewall Permission

**Affected rule:** Wi-Fi Direct Spooler Use (In)

**Observed configuration:**

- Enabled: True
- Direction: Inbound
- Action: Allow
- Profile: Public
- Protocol: Any
- Local port: Any
- Remote address: Any
- Interface type: Any
- Program: `C:\Windows\System32\spoolsv.exe`

### Security Concern

The firewall rule allows matching incoming traffic on Public networks and has several broad-looking filter settings.

If the computer does not require Wi-Fi Direct printing, this permission may be unnecessary.

Unnecessary inbound permissions can increase potential exposure, although the investigation did not demonstrate that this particular rule was exploitable or reachable from an external network.

### Evidence Supporting Legitimacy

- The rule referenced the standard Windows Print Spooler executable path.
- The executable's digital signature was valid.
- The signing certificate identified Microsoft.
- The Print Spooler was registered and running as a Windows service.

### Evidence Limitations

The investigation did not establish:

- Whether Wi-Fi Direct printing was required by the computer owner.
- Every remaining condition attached to the firewall rule.
- Whether the Print Spooler had a listening TCP or UDP endpoint.
- Whether the rule was reachable from another device.
- Whether any unauthorised connection had occurred.
- Whether an exploitable vulnerability existed.

**Assessment:** Potentially unnecessary firewall permission requiring configuration review. No confirmed compromise.

---

## 6. Recommendations

1. **Confirm the business requirement.** Ask the computer owner whether Wi-Fi Direct printing or related functionality is required.
2. **Review the complete firewall rule.** Confirm whether additional service, interface or other conditions restrict its use.
3. **Apply least privilege where appropriate.** If the permission is unnecessary, consider restricting or disabling the specific rule after evaluating the operational impact and obtaining approval.
4. **Avoid unnecessary service changes.** Do not disable the Print Spooler solely because this firewall rule exists.
5. **Recheck after approved changes.** Verify the effective firewall configuration and confirm that required printing functions continue to work.

No firewall rules or Windows services were changed during this project.

---

## 7. Final Conclusion

This investigation reviewed Windows Firewall settings and examined a printing-related inbound Allow rule on the Public network profile.

The effective Public firewall policy blocked inbound traffic by default and allowed outbound traffic by default.

The selected printing rule was enabled and associated with the Windows Print Spooler executable, which had a valid Microsoft digital signature.

Although the rule's inspected settings were broad, the investigation did not confirm a security breach, an exposed network service, or an exploitable vulnerability.

**Final finding:** A potentially unnecessary inbound firewall permission was identified for further review.

The recommended next action is to confirm whether Wi-Fi Direct printing is required before considering changes to the rule.

---

## 8. Skills Demonstrated

- Windows Firewall configuration auditing
- PowerShell command execution
- Active firewall policy inspection
- Inbound and outbound traffic analysis
- Firewall rule investigation
- PowerShell error troubleshooting
- Windows service investigation
- Digital signature verification
- Network listening-port inspection
- Evidence-based risk assessment
- Security documentation and reporting

## 9. Key Lessons Learned

This project reinforced the importance of distinguishing between security configurations and confirmed security incidents.

An enabled firewall rule does not automatically indicate a vulnerability.

A listening network port does not automatically indicate a successful connection.

A valid digital signature supports file authenticity but does not guarantee that software cannot be misused.

Most importantly, a cybersecurity analyst should **collect evidence, understand its limitations, and recommend proportionate actions rather than make unsupported claims**.

---

**Project status:** Completed — Initial investigation and assessment  
**Changes made to system:** None  
**Case classification:** Firewall configuration review; no confirmed security incident
