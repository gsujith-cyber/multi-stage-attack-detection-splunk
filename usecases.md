# Use Cases – Multi-Stage Attack Detection using Splunk

This document outlines security use cases implemented to detect a multi-stage attack using Splunk, mapped to MITRE ATT&CK framework.

---

## 1. Brute Force Attack Detection

**Description:**  
Detect repeated failed login attempts from a user or IP address.

**Event ID:** 4625  
**MITRE Technique:** T1110 – Brute Force  

**Detection Logic:**  
- Monitor high number of failed login attempts  
- Identify abnormal login behavior  

**Impact:**  
May lead to account compromise.

---

## 2. Successful Login After Brute Force

**Description:**  
Detect successful authentication following multiple failed attempts.

**Event ID:** 4624  
**MITRE Technique:** T1078 – Valid Accounts  

**Detection Logic:**  
- Correlate failed and successful login events  
- Identify suspicious login success  

**Impact:**  
Indicates unauthorized access.

---

## 3. Suspicious Process Execution

**Description:**  
Detect execution of PowerShell or suspicious processes.

**Event ID:** 4688  
**MITRE Technique:** T1059 – Command and Scripting Interpreter  

**Detection Logic:**  
- Monitor process creation logs  
- Filter for PowerShell execution  

**Impact:**  
Indicates attacker command execution.

---

## 4. User Creation and Privilege Escalation

**Description:**  
Detect creation of a new user and elevation to admin privileges.

**Event IDs:** 4720, 4728  
**MITRE Techniques:**  
- T1136 – Create Account  
- T1098 – Account Manipulation  

**Detection Logic:**  
- Identify new user accounts  
- Detect addition to Domain Admins group  

**Impact:**  
Grants attacker full administrative control.

---

## 5. Persistence Mechanism Detection

**Description:**  
Detect scheduled task creation.

**Event ID:** 4698  
**MITRE Technique:** T1053 – Scheduled Task/Job  

**Detection Logic:**  
- Monitor scheduled task creation  
- Identify suspicious tasks  

**Impact:**  
Attacker maintains long-term access.

---

## 6. Attack Timeline Correlation

**Description:**  
Correlate events to reconstruct attack sequence.

**MITRE Mapping:** Multiple techniques across attack lifecycle  

**Detection Logic:**  
- Combine multiple event IDs over time  
- Visualize attack progression  

**Impact:**  
Provides full visibility of attack lifecycle.

---

## Conclusion

These use cases demonstrate detection of a complete multi-stage attack aligned with the MITRE ATT&CK framework, covering initial access, execution, privilege escalation, and persistence.
