# (WIP) Devices-Accidentally-Exposed-to-the-Internet
Devices Accidentally Exposed to the Internet (Threat Hunt)


# Scenario 1: Devices Accidentally Exposed to the Internet

## Overview
This project simulates an incident response scenario where virtual machines (VMs) are unintentionally exposed to the public internet. The goal is to analyze security logs, detect potential threats, and implement mitigation strategies.

---

## Prerequisites
- A VM onboarded to **Microsoft Defender for Endpoint (MDE)**.
- The VM was running for 12+ hours to produce logs.

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
  - ### Which devices were exposed to the internet?
    The EDR-test-vm was internet facing at this time: Feb 19th 12:07pm to Feb 20th 1:12am
 ![image](https://github.com/user-attachments/assets/087cd60b-3257-4767-8f55-5d356f5f7d57)

    
  - ### Excessive failed login attempts? Source IP addresses and frequency of login failures?
      ![image](https://github.com/user-attachments/assets/c59d825a-ef3d-4a89-b900-db30c237d57d)

    ### After locating the bad actor's IP addresses I ran a query to check to see if there were any successful logins
    ![image](https://github.com/user-attachments/assets/18b6fb9f-dba1-4de6-88fe-0e9f10315bdf)

    ### Checking correct user name and failed log in attempts, indication if bad actor has the right account name
    ![image](https://github.com/user-attachments/assets/72e043ca-213d-40be-8f7c-94c5f9c3f915)






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

