# Brute Force Attack Detection - SOC Lab

## Overview
In this lab, I analyzed web server logs to identify suspicious login activity. The i nvestigation revealed multiple failed login attemps followed by a successful authentication from the same external Ip address.

This behavior is consistent with a brute force attack resulting in unauthorized access.

---

## Scenario
A security alert was triggered indicating a posible suspicious login attempt from an external IP address.

The following logs were analyzed:
```
192.168.1.10 -- [12/Mar/20226:10:15:32] "GET /login HTTP/1.1" 200
185.234.217.55 -- [12/Mar/20226:10:16:01] "POST /login HTTTP/1.1" 401
185.234.217.55 -- [12/Mar/20226:10:16:05] "POST /login HTTTP/1.1" 401
185.234.217.55 -- [12/Mar/20226:10:16:07] "POST /login HTTTP/1.1" 401
185.234.217.55 -- [12/Mar/20226:10:16:10] "POST /login HTTTP/1.1" 200
185.234.217.55 -- [12/Mar/20226:10:16:15] "GET /login HTTTP/1.1" 200
```

---

## Incident Report

### Summary
Multiple failed login attemps ere detected from an external IP address, followed by a successful authentication and access to the dashboard. This behavior is consistent with a potential brute force attack resulting in unauthorizaed access.

### Evidence
- Source IP: 185.234.217.55
- Multiple failed login attemps (HTTP 401) within seconds:
  - 10:16:01
  - 10:16:05
  - 10:16:07
- Successful login (HTTTP 200) at 10:16:10
- Subsequent access ti /dashboard at 10:16:15
- Rapid sequence of login attemps within a short time frame

### Analysis
The logs show a pattern of repeated failed login attemps followed by a successful authentication from the same external IP address. The short time intervals between attemps suggest automated behavior rather than human input. This pattern is commoly associated with brute force attacks, where multiple password combinations are tested until valid credentials are found. The successful login indicates that the attacker likely compromised valid user credentials.

### Conclusion
This incident is indicative of a successfulbrute force attack resulting in anauthorized acess ti the system.

### Recommendation
- Immediately block or restrict the source IP address (185.234.217.55)
- Force password reset for the affected account(s)
- Enable Multi-Factor Authentication (MFA)
- Review recent user activity for suspicious actions
- Implement account lockout policies after multiple failed login attemps

---

## Skil Demonstrated
- Log analysis
- Threat detection
- Incident investigation
- SOC reporting
- Brute force attack identification

---

## Tools Used
- Manual log analysis (simulating SOC environment)

---

## Key Takeaway
This lab demonstrates how analyzing login patterns and HTTP status codes can help identify brute force attacks and unauthorized access in real-world scenarios.

