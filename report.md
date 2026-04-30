# Multi-Stage Attack Detection Report using Splunk

## 1. Introduction
This report presents the detection and analysis of a simulated multi-stage cyber attack using Splunk. The objective is to identify different phases of the attack by analyzing Windows security logs and correlating events with the MITRE ATT&CK framework.

---

## 2. Objective
- Detect brute force attacks  
- Identify successful compromise  
- Monitor suspicious command execution  
- Detect privilege escalation  
- Identify persistence mechanisms  
- Reconstruct attack timeline  

---

## 3. Tools Used
- Splunk Enterprise  
- Windows Security Logs  

---

## 4. Attack Overview
The attack follows a multi-stage pattern:

1. Brute force login attempts  
2. Successful login  
3. Command execution (PowerShell)  
4. User creation  
5. Privilege escalation  
6. Persistence via scheduled task  

---

## 5. Attack Detection and MITRE Mapping

### 5.1 Brute Force Attack
- **Event ID:** 4625  
- **Description:** Multiple failed login attempts detected  
- **MITRE Technique:** T1110 – Brute Force  

**Analysis:**  
Repeated failed logins from the same source indicate a brute force attack targeting user credentials.

---

### 5.2 Successful Login (Compromise)
- **Event ID:** 4624  
- **Description:** Successful login after multiple failures  
- **MITRE Technique:** T1078 – Valid Accounts  

**Analysis:**  
The attacker successfully authenticated using compromised credentials.

---

### 5.3 Suspicious Process Execution
- **Event ID:** 4688  
- **Description:** PowerShell execution detected  
- **MITRE Technique:** T1059 – Command and Scripting Interpreter  

**Analysis:**  
Execution of PowerShell indicates potential attacker activity and command execution.

---

### 5.4 User Creation and Privilege Escalation
- **Event IDs:** 4720, 4728  
- **Description:**  
  - New user account 'hacker' created  
  - User added to Domain Admins group  
- **MITRE Techniques:**  
  - T1136 – Create Account  
  - T1098 – Account Manipulation  

**Analysis:**  
The attacker created a new account and elevated privileges to gain administrative control over the system.

---

### 5.5 Persistence Mechanism
- **Event ID:** 4698  
- **Description:** Scheduled task creation detected  
- **MITRE Technique:** T1053 – Scheduled Task/Job  

**Analysis:**  
The attacker established persistence by creating a scheduled task to maintain access.

---

### 5.6 Attack Timeline Analysis
- **MITRE Coverage:** Multiple techniques across attack lifecycle  

**Analysis:**  
Events were correlated over time using Splunk to reconstruct the full attack sequence. The timeline clearly shows progression from brute force to persistence.

---

## 6. Dashboard Analysis
A Splunk dashboard was created to visualize:

- Failed login attempts (Brute force detection)  
- Successful logins (Compromise detection)  
- Attack timeline (Event correlation)  
- Event distribution (Activity overview)  

This enables real-time monitoring and faster identification of suspicious behavior.

---

## 7. Impact
- Unauthorized access to system accounts  
- Privilege escalation to administrative level  
- Execution of malicious commands  
- Creation of backdoor user accounts  
- Persistence within the system  
- Potential full system compromise  

---

## 8. Mitigation
- Implement strong password policies and account lockout mechanisms  
- Monitor failed login attempts and suspicious login activity  
- Restrict and monitor PowerShell execution  
- Apply least privilege principle  
- Monitor user creation and privilege changes  
- Regularly review scheduled tasks  
- Use SIEM solutions like Splunk for continuous monitoring  

---

## 9. Conclusion
This project demonstrates how multi-stage cyber attacks can be detected using Splunk by analyzing Windows security logs and mapping activities to the MITRE ATT&CK framework. 

By correlating events across different stages, it is possible to reconstruct the attack lifecycle and detect advanced threats effectively. The project highlights key SOC skills such as log analysis, threat detection, event correlation, and incident investigation.
