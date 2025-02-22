# Devices Accidentally Exposed to the Internet (Threat Hunt)

## Scenario 1: Devices Accidentally Exposed to the Internet

### Overview
This project simulates an incident response scenario in which virtual machines (VMs) are unintentionally exposed to the public Internet. The goal is to analyze security logs, detect potential threats, and implement mitigation strategies.

---

### Prerequisites
- A VM onboarded to **Microsoft Defender for Endpoint (MDE)**.
- The VM ran for 12+ hours to generate logs.

---

### Data Collection

**Goal:** Gather relevant data from logs, network traffic, and endpoints.

- **Which devices were exposed to the Internet?**  
  The EDR-test-vm was Internet-facing from February 19th, 12:07 PM to February 20th, 1:12 AM.  
  ![Exposure Timeline](https://github.com/user-attachments/assets/087cd60b-3257-4767-8f55-5d356f5f7d57)

- **Excessive Failed Login Attempts:**  
  Analysis of source IP addresses and the frequency of login failures.  
  ![Failed Login Attempts](https://github.com/user-attachments/assets/c59d825a-ef3d-4a89-b900-db30c237d57d)

- **Query for Successful Logins:**  
  After locating the bad actor's IP addresses, a query was run to check for any successful logins.  
  ![Successful Logins Query](https://github.com/user-attachments/assets/18b6fb9f-dba1-4de6-88fe-0e9f10315bdf)

- **Username Verification:**  
  Verified the correct username in relation to the failed login attempts to determine if the bad actor had the right account name.  
  ![Username Verification](https://github.com/user-attachments/assets/72e043ca-213d-40be-8f7c-94c5f9c3f915)

- **Review of Successful Login IP Addresses:**  
  Checked all successful login IP addresses for the labuser to determine if any were unusual or from unexpected locations. All were normal.  
  <img width="794" alt="Successful Login IP Addresses" src="https://github.com/user-attachments/assets/d3f91b7f-2f70-4e14-8491-0f11034814e7" />

---

### MITRE ATT&CK Techniques Identified

- **T1110 – Brute Force**
  - *Sub-technique: T1110.001 – Password Guessing*

**Context:**
- The device was accidentally exposed to the Internet, which allowed remote login attempts.
- Logs indicate excessive failed logins and subsequent verification of source IP addresses and user accounts.

---

### Response Actions
- Hardened the NSG attached to EDR-Test-VM to allow only RDP traffic from specific endpoints (no public Internet access).
- Implemented an account lockout policy.
- Implemented multi-factor authentication (MFA).
