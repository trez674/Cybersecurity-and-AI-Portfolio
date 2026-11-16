# Cybersecurity Project 3 — Windows Security Audit and Threat Detection

## Project Overview

This project involved performing a read-only security audit of a Windows computer using built-in Windows Security and Settings tools.

The purpose was to assess the computer's security configuration, identify potential risks, examine available threat detection history, and recommend improvements.

**Audit type:** Local Windows security configuration assessment  
**Method:** Manual, read-only inspection  
**Technical checks completed:** 34  
**Changes made:** None

## Project Objectives

- Examine Windows antivirus and firewall protection.
- Review account security and access controls.
- Investigate ransomware protection.
- Inspect network discovery and sharing settings.
- Review application and browser security.
- Identify security improvement opportunities.
- Practise documenting evidence and communicating findings.

## Tools Used

- Windows Security
- Microsoft Defender Antivirus
- Microsoft Defender Firewall
- Windows Settings
- Microsoft Defender SmartScreen
- Controlled Folder Access

## Audit Findings

| Step | Security Control | Observed Result |
|---|---|---|
| 1 | Windows Security overview | All green indicators |
| 2 | Real-time protection | On |
| 3 | Defender Protection History | No recent actions |
| 4 | Active network and firewall | Private; firewall On |
| 5 | Windows Update | Up to date |
| 6 | Check apps and files | On |
| 7 | Memory integrity | On |
| 8 | Windows Hello | Not set up |
| 9 | Defender Security Intelligence | Up to date |
| 10 | User Account Control | Level 3 — Default |
| 11 | Account type | Administrator |
| 12 | Sign-in after absence | Every time |
| 13 | Plugged-in sleep timeout | 5 minutes or less |
| 14 | Device encryption | On |
| 15 | Windows Backup | Not configured |
| 16 | OneDrive synchronisation | Up to date |
| 17 | Remote Desktop | Off |
| 18 | Private Network Discovery | On |
| 19 | Private File and Printer Sharing | Off |
| 20 | Public File and Printer Sharing | Off |
| 21 | Public Network Discovery | Off |
| 22 | Public network firewall | On |
| 23 | Tamper Protection | On |
| 24 | Controlled Folder Access | On |
| 25 | Protected folders | Folders listed; names not recorded |
| 26 | Allowed applications | None listed |
| 27 | Controlled Folder Access block history | No blocked events shown |
| 28 | Cloud-delivered protection | On |
| 29 | Automatic sample submission | On |
| 30 | Potentially unwanted app blocking | On |
| 31 | Block apps | Ticked |
| 32 | Block downloads | Ticked |
| 33 | SmartScreen for Microsoft Edge | On |
| 34 | SmartScreen for Microsoft Store apps | On |

## Positive Security Findings

The computer had several important protections enabled, including:

- Microsoft Defender real-time antivirus protection.
- Up-to-date security intelligence.
- Microsoft Defender Firewall for Private and Public networks.
- Device encryption and memory integrity.
- Tamper Protection.
- Controlled Folder Access.
- Cloud-delivered protection.
- Potentially unwanted application blocking.
- Microsoft Defender SmartScreen for Edge and Store apps.

Remote Desktop and Public network discovery were disabled, reducing unnecessary network exposure.

## Potential Risks and Recommendations

### 1. Backup and Recovery — Priority: High

**Finding:** Windows Backup was not configured, although OneDrive synchronisation was up to date.

**Risk:** Cloud synchronisation alone does not guarantee independent, recoverable backups. Deletions and unwanted changes may synchronise.

**Recommendation:** Verify existing backups and consider an independent backup solution with periodic restoration testing.

### 2. Administrator Privileges — Priority: Medium

**Finding:** The inspected Windows account had Administrator privileges.

**Risk:** Everyday use of an administrator account can increase the impact of malicious software or accidental system changes.

**Recommendation:** Consider using a standard user account for routine work and reserving administrator privileges for maintenance.

### 3. Private Network Discovery — Priority: Low / Context-dependent

**Finding:** Network Discovery was enabled on the Private network profile.

**Risk:** The computer may be more discoverable to other devices on the local network.

**Recommendation:** Determine whether discovery is required. If unnecessary, consider disabling it after reviewing network-sharing requirements.

### 4. Windows Hello — Priority: Optional Improvement

**Finding:** Windows Hello was not configured.

**Consideration:** Windows Hello can provide a convenient sign-in option, but its absence alone does not prove that the existing sign-in method is insecure.

**Recommendation:** Review available Windows Hello sign-in options and assess whether they would improve the device's authentication experience.

## Threat Detection Review

Microsoft Defender Protection History displayed no recent actions.

Controlled Folder Access block history displayed no blocked events.

These findings indicate that no relevant events were visible in the inspected histories. They do not establish that the system has never experienced malicious activity.

This project was a configuration audit with limited threat-history inspection, not a full forensic investigation or penetration test.

## CIA Triad Connections

**Confidentiality:** Device encryption, authentication and browser protections help safeguard sensitive information.

**Integrity:** Tamper Protection, Controlled Folder Access and antivirus protection help prevent unauthorised changes.

**Availability:** Ransomware protection and reliable backup arrangements help reduce the risk of data becoming unavailable.

## Skills Demonstrated

- Windows security auditing
- Antivirus and firewall configuration review
- Basic ransomware protection assessment
- Network security inspection
- Access control and least-privilege awareness
- Threat history investigation
- Security risk identification
- Technical documentation and reporting

## Final Conclusion

The Windows computer demonstrated generally positive security configurations across the 34 checks performed.

No immediate evidence of compromise was identified in the limited security histories inspected. However, the audit cannot establish that the computer is completely secure or free from threats.

The most important follow-up is to verify a reliable backup and recovery strategy. Additional improvements may include reviewing administrator privileges, Windows Hello and Private Network Discovery.

**Project outcome:** Completed a structured, read-only Windows security audit and documented findings, limitations and practical recommendations.
