# Project 4 — Windows Event Logs & Threat Investigation

## Project Overview

This project involved investigating Windows Security event logs using Event Viewer to identify and analyse potential security threats. I examined authentication activity, compared security events and assessed whether the evidence indicated unauthorised access.

## Tools Used

- **Windows Event Viewer** — Examined and filtered security events.
- **Windows Security Logs** — Investigated authentication activity.
- **Event IDs 4624, 4625, 4672 and 5379** — Reviewed successful and failed logons, privileged logons and credential-related events.

## Key Findings

I investigated two failed login events (Event ID **4625**) recorded on **11 November 2026 at 00:17:57 and 00:17:59**.

Both events shared the following characteristics:

- **Account:** Same Windows user account
- **Logon Type:** 2 — Interactive
- **Failure Reason:** Unknown user name or bad password
- **Caller Process ID:** `0xca0` (3232 decimal)
- **Caller Process:** Apparently the same `svchost.exe` executable path
- **Source Network Address:** Local loopback information; the event at 00:17:59 recorded `127.0.0.1`

The matching details suggest that the two authentication failures may be related.

## Risk Assessment

The events occurred two seconds apart and shared several authentication characteristics. However, the evidence was insufficient to confirm a cyberattack or unauthorised access.

**Assessment:** Potentially suspicious authentication activity, with no confirmed security compromise.

## Recommendations

- Monitor Windows Security logs for repeated failed login attempts.
- Correlate failed logins with successful logins to identify unusual activity.
- Investigate the responsible Windows service if authentication failures continue.
- Maintain strong passwords and appropriate account security controls.

## Conclusion

This project developed my practical skills in Windows Event Viewer, security monitoring, evidence correlation and threat assessment.

I learned how to investigate authentication events, identify patterns and document findings without assuming that every failed login indicates a cyberattack.
