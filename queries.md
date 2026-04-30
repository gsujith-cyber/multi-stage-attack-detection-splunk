# Splunk Queries – Multi-Stage Attack Detection

This document contains the Splunk queries used to detect each stage of the attack.

---

## 1. Raw Logs

```spl
index=security
```

---

## 2. Failed Login Attempts (Brute Force Detection)

```spl
index=security EventCode=4625
| stats count by Account_Name, src_ip
| sort -count
```

---

## 3. Successful Login Detection

```spl
index=security EventCode=4624
| stats count by Account_Name
| sort -count
```

---

## 4. PowerShell Execution Detection

```spl
index=security EventCode=4688
| search powershell
| table _time Account_Name New_Process_Name
```

---

## 5. User Creation and Privilege Escalation

```spl
index=security (EventCode=4720 OR EventCode=4728)
| table _time Account_Name EventCode
```

---

## 6. Persistence Mechanism (Scheduled Task)

```spl
index=security EventCode=4698
| table _time Account_Name Task_Name
```

---

## 7. Attack Timeline

```spl
index=security sourcetype=windows_security_lab 
(EventCode=4625 OR EventCode=4624 OR EventCode=4688 OR EventCode=4720 OR EventCode=4728 OR EventCode=4698)
| eval Event_Type=case(
    EventCode=4625,"Failed Login",
    EventCode=4624,"Successful Login",
    EventCode=4688,"Process Execution",
    EventCode=4720,"User Creation",
    EventCode=4728,"Privilege Escalation",
    EventCode=4698,"Persistence"
)
| timechart count by Event_Type
```

---

## 8. Dashboard Queries

### Failed Login Panel
```spl
index=security EventCode=4625
| stats count by Account_Name
```

### Successful Login Panel
```spl
index=security EventCode=4624
| stats count by Account_Name
```

### Timeline Panel
```spl
index=security
| timechart count by EventCode
```

### Event Distribution Panel
```spl
index=security
| stats count by EventCode
```

---

## Notes

- EventCode 4625 → Failed login (Brute force)  
- EventCode 4624 → Successful login  
- EventCode 4688 → Process execution  
- EventCode 4720 → User creation  
- EventCode 4728 → Privilege escalation  
- EventCode 4698 → Persistence (Scheduled Task)  
