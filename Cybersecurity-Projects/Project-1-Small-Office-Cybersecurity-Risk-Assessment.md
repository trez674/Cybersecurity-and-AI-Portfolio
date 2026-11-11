# Project 1 — Small Office Cybersecurity Risk Assessment

## 1. Project Overview

In this project, I carried out a simulated cybersecurity risk assessment of a small office network.

The aim was to identify potential security threats, vulnerabilities and risks, and recommend suitable security controls to protect the network.

This assessment builds on my previous project, **Project 4 — Small Office Network Design**.

**Project type:** Scenario-based cybersecurity risk assessment.

**Important:** The weaknesses described in this report are fictional scenarios created for learning. They are not confirmed vulnerabilities in real devices.

## 2. Project Objectives

- Understand the difference between threats, vulnerabilities and risks.
- Identify common security weaknesses in a small office.
- Recommend appropriate security controls.
- Understand the CIA Triad.
- Assess risks using likelihood and impact.
- Practise documenting cybersecurity findings.

## 3. Office Network Overview

The fictional office network contains:

- 1 Wi-Fi router
- 1 network switch
- 4 wired desktop computers
- 1 network printer
- 1 wireless laptop
- An internet connection

The planned network uses the subnet `192.168.10.0/24`, with the router's LAN IP address set to `192.168.10.1`.

The office network is a design exercise rather than a physically deployed network.

## 4. Cybersecurity Concepts

### Threat

A threat is something that could cause harm to a system, network or organisation.

Examples include cybercriminals, malware, hardware failure and accidental data deletion.

### Vulnerability

A vulnerability is a weakness that could be exploited or contribute to a security incident.

Examples include weak passwords, unsupported software and missing backups.

### Risk

Risk concerns the possibility of harm and its consequences.

For example, a weak router administrator password could increase the risk of unauthorised changes to network settings.

### Security Control

A security control is a measure used to prevent, detect or reduce security risks.

Examples include strong passwords, software updates, access restrictions and tested backups.

## 5. The CIA Triad

The CIA Triad represents three important cybersecurity principles.

| Principle | Meaning | Example |
|---|---|---|
| Confidentiality | Protecting information from unauthorised access | Restricting access to customer records |
| Integrity | Protecting information and settings from unauthorised changes | Preventing unauthorised router configuration changes |
| Availability | Keeping systems and information accessible when needed | Maintaining working backups and recovery procedures |

A single security incident may affect more than one principle.

## 6. Simulated Risk Assessment

The following findings are hypothetical examples for the fictional office.

### Risk 1 — Weak Router Administrator Password

**Asset:** Office Wi-Fi router

**Threat:** Unauthorised person attempting to access the router's administration interface.

**Vulnerability:** Weak administrator password.

**Possible impact:** An attacker could change network settings, including DNS configuration, potentially disrupting services or redirecting traffic.

**CIA principles affected:** Integrity, with possible confidentiality and availability consequences.

**Recommended security controls:**
- Configure a strong, unique administrator password.
- Restrict access to the router's management interface.
- Keep router firmware updated.
- Enable multifactor authentication if supported.

### Risk 2 — Unprotected Printer Management Interface

**Asset:** Network printer

**Threat:** Unauthorised user attempting to change printer settings.

**Vulnerability:** The printer's management interface does not require administrator authentication.

**Possible impact:** Printer settings could be changed without permission, potentially disrupting printing or exposing information.

**CIA principles affected:** Integrity, with possible confidentiality and availability consequences.

**Recommended security controls:**
- Set a strong administrator password.
- Restrict management access to authorised users or devices.
- Install supported printer firmware updates.
- Disable unnecessary services.

### Risk 3 — Missing File Backups

**Asset:** Office computers and important business files

**Threat:** Hardware failure, accidental deletion, malware or other data-loss events.

**Vulnerability:** Important files are not backed up.

**Possible impact:** Business information could be permanently lost, interrupting operations.

**CIA principle affected:** Availability, with possible integrity consequences.

**Recommended security controls:**
- Create regular backups.
- Store protected backup copies separately from the original systems.
- Test that files can be restored.
- Document a recovery procedure.

### Risk 4 — Unsupported Operating System

**Asset:** Office desktop computer

**Threat:** Malware or attackers exploiting known security weaknesses.

**Vulnerability:** An operating system that no longer receives security updates.

**Possible impact:** Unauthorised access, malware infection or compromise of company information.

**CIA principles affected:** Confidentiality, integrity and availability.

**Recommended security controls:**
- Upgrade to a supported operating system.
- Install security updates promptly.
- Use appropriate endpoint protection.
- Restrict unnecessary administrator privileges.

## 7. Risk Prioritisation

Risk levels can be estimated by considering likelihood and impact.

For this classroom exercise, the following ratings are illustrative assumptions rather than measurements from a real organisation.

| Risk | Assumed Likelihood | Assumed Impact | Priority |
|---|---|---|---|
| Weak router administrator password | Medium | High | High |
| Unprotected printer management | Medium | Medium | Medium |
| Missing backups | High | High | High |
| Unsupported operating system | High | High | High |

The highest-priority risks should receive attention first.

A real risk assessment would require evidence about the organisation, its existing security controls, the likelihood of each scenario and the potential business impact.

## 8. Recommended Action Plan

1. **Protect router administration:** Replace weak credentials and restrict management access.
2. **Implement backups:** Protect important files and test recovery.
3. **Update unsupported computers:** Move to supported software and apply security patches.
4. **Secure printer management:** Require authentication and limit administrative access.
5. **Review security regularly:** Reassess risks when devices, software or business requirements change.

## 9. Skills Developed

Through this project, I practised:

- Identifying cybersecurity threats
- Recognising vulnerabilities
- Describing potential risks
- Recommending security controls
- Applying the CIA Triad
- Estimating likelihood and impact
- Prioritising security improvements
- Writing a basic cybersecurity risk assessment

## 10. Conclusion

This project helped me understand how cybersecurity professionals identify and assess security weaknesses in a small office environment.

I learned that a threat, vulnerability and risk are different concepts, and that security controls help reduce the likelihood or impact of harmful events.

I also learned how confidentiality, integrity and availability relate to everyday business systems.

The assessment was based on fictional scenarios and did not involve scanning, exploiting or testing real devices.

My next learning goal is to understand access control, authentication and how organisations restrict access to sensitive systems and information.
