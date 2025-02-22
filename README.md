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

## Data Collection
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


    ### Checked all successful login IP addresses for the labuser to see if any of them were unusual or from an un expected location. All were normal
    <img width="794" alt="image" src="https://github.com/user-attachments/assets/d3f91b7f-2f70-4e14-8491-0f11034814e7" />



---


## **MITRE ATT&CK Techniques Identified:**

- **T1110 – Brute Force**
  - *Sub-technique: T1110.001 – Password Guessing*

**Context:**
- Device accidentally exposed to the Internet allowed remote login attempts.
- Logs indicate excessive failed logins and subsequent verification of source IPs and user accounts.

---
# Response Actions:
- Hardened the NSG attached to EDR-Test-Vm to allow only RDP traffic from specific endpoints (no public internet access)
- Implemented account lockout policy
- Implemented MFA 

