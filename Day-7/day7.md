# 🎄 Advent of Cyber 2025 — Day 7  
<img src="./images/day7-banner.png" width="900"/>

**Title:** Network Discovery - Scan-ta Clause 
**Date Completed:** Dec 2025  
**Difficulty:** Easy–Medium  
**Category:** Network Scanning, Service Enumeration  
**Room Link:** [Network Discovery - Scan-ta Clause](https://tryhackme.com/room/networkservices-aoc2025-jnsoqbxgky)
**Status:** ✔ Completed  

---

## 🧭 Overview  
HopSec has breached the TBFC QA environment and locked everyone out.  
Your objective: **discover exposed services, recover hidden keys, access the admin panel, and restore tbfc-devqa01**.

This room focuses on **Nmap**, TCP/UDP scanning, and identifying hidden services across ports 1–65535.

---

# 🧩 Task-by-Task Write-Up

---

## **🔍 Service Discovery with Nmap**

### **1. Basic Scan**
```
nmap MACHINE_IP
```

Open ports found:
- **22/tcp — SSH**
- **80/tcp — HTTP**

The HTTP page shows a defacement:

**Pwned by HopSec**

---

## **🔎 Full Scan (-p-) + Banner Grabbing**
```
nmap -p- --script=banner MACHINE_IP
```

Additional open ports discovered:

| Port | Service | Info |
|------|----------|------|
| 21212/tcp | FTP | vsFTPd 3.0.5 |
| 25251/tcp | custom | TBFC maintd v0.2 |
| 53/udp | DNS | domain |

These hidden services contain the **3 key parts** needed to access the QA admin console.

---

# 🧩 Key Discovery

---

## **1️⃣ KEY PART 1 — FTP (Port 21212)**  
Anonymous login worked:

```
ftp MACHINE_IP 21212
ls
get tbfc_qa_key1
```

Found:

```
3aster_
```

---

## **2️⃣ KEY PART 2 — TBFC maintd App (Port 25251)**  
Use Netcat:

```
nc -v MACHINE_IP 25251
HELP
GET KEY
```

Returned:

```
15_th3_
```

---

## **3️⃣ KEY PART 3 — DNS (UDP 53)**  
Query TXT record:

```
dig @MACHINE_IP TXT key3.tbfc.local +short
```

Result:

```
n3w_xm45
```

---

# 🧩 Admin Console Access  
Combine all three key parts:

```
3aster_15_th3_n3w_xm45
```

Enter this on the web admin panel at:

```
http://MACHINE_IP
```

This unlocks the **Secret Admin Console**, giving terminal access.

---

# 🛠 On-Host Enumeration  
Now inside the server, list listening ports:

```
ss -tunlp
```

Reveals MySQL running on port **3306**.

Connect locally without a password:

```
mysql -D tbfcqa01 -e "show tables;"
mysql -D tbfcqa01 -e "select * from flags;"
```

Flag:

```
THM{4ll_s3rvice5_d1sc0vered}
```

---

# 🏁 Final Answers

| Question | Answer |
|----------|--------|
| Evil message on the website | **Pwned by HopSec** |
| First key (FTP) | **3aster_** |
| Second key (TBFC app) | **15_th3_** |
| Third key (DNS) | **n3w_xm45** |
| MySQL port | **3306** |
| Final flag | **THM{4ll_s3rvice5_d1sc0vered}** |

---

# 🎯 Learning Objectives Achieved  
- Performed TCP/UDP service discovery with Nmap  
- Identified hidden services beyond common ports  
- Interacted with unknown services via Netcat  
- Queried DNS TXT records  
- Used on-host enumeration to retrieve flags  
- Combined multi-source intel to regain access  

---

# 📘 What I Learned Today  
> “Network discovery is often the first step to regaining control — every open port is a clue.”

---

# 🔜 Next Step  
Begin **Day 8** and continue hunting the HopSec bunnies.


