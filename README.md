# Devices-Accidentally-Exposed-to-the-Internet
Devices Accidentally Exposed to the Internet (Threat Hunt)


# Scenario 1: Devices Accidentally Exposed to the Internet

## Overview
This project simulates an incident response scenario where virtual machines (VMs) are unintentionally exposed to the public internet. The goal is to analyze security logs, detect potential threats, and implement mitigation strategies.

---

## Prerequisites
- A VM onboarded to **Microsoft Defender for Endpoint (MDE)**.
- The VM should remain active for **90 minutes** to attract potential threats from malicious actors and bots.
- Alternatively, use the pre-existing honeypot VM: **windows-target-1**.

---

## 1. Preparation
**Goal:** Define the scope of the security investigation.

- Investigate any misconfigured VMs within the shared services cluster (DNS, Domain Services, DHCP, etc.).
- Identify brute-force login attempts from external sources.
- Formulate a hypothesis based on potential attack vectors, e.g., **"Could there be lateral movement in the network?"**
- Consider older devices without account lockout policies, which may have been exploited via brute-force attacks.

---

## 2. Data Collection
**Goal:** Gather relevant data from logs, network traffic, and endpoints.

- Analyze logs to determine:
  - Which devices were exposed to the internet.
  - Excessive failed login attempts.
  - Source IP addresses and frequency of login failures.
- Ensure logs are available from key sources:
  - `DeviceInfo`
  - `DeviceLogonEvents`

---

## 3. Data Analysis
**Goal:** Identify anomalies, patterns, and potential Indicators of Compromise (IoCs).

- Look for evidence of **brute-force login success** (multiple failed attempts followed by a successful login).
- Investigate further activity on compromised machines.
- Identify whether unauthorized users gained access.

---

## 4. Investigation
**Goal:** Assess the scope of the detected threats.

- Examine suspicious findings in relation to **MITRE ATT&CK Tactics, Techniques, and Procedures (TTPs)**.
- Use external threat intelligence sources and logs to confirm indicators of compromise.
- Reference available MITRE ATT&CK documentation:
  - [MITRE ATT&CK Framework](https://attack.mitre.org/)

---

## 5. Response
**Goal:** Contain, remove, and recover from the threat.

- Work with security teams to **isolate** affected systems.
- Implement **remediation steps** to prevent further exploitation.
- Identify security misconfigurations and apply necessary patches.

---

## 6. Documentation
**Goal:** Record all findings and lessons learned.

- Document:
  - **Initial findings**
  - **Investigative steps taken**
  - **Actions performed**
  - **Root cause analysis**
- Use findings to improve future security hunts.

---

## 7. Improvement
**Goal:** Enhance security posture for future threat detection.

- Identify security gaps and refine detection methods.
- Implement **better access control** and **logging policies**.
- Evaluate:
  - **Could the attack have been prevented?**
  - **How can the investigation process be optimized?**

---

## Sample Queries
### Check most failed logins:
```kusto
DeviceLogonEvents
| where LogonType has_any("Network", "Interactive", "RemoteInteractive", "Unlock")
| where ActionType == "LogonFailed"
| where isnotempty(RemoteIP)
| summarize Attempts = count() by ActionType, RemoteIP, DeviceName
| order by Attempts
