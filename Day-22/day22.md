# 🎄 Advent of Cyber 2025 — Day 22  
<img src="./images/day22-banner.png" width="900"/>
**Title:** C2 Detection - Command & Carol      
**Difficulty:** Medium  
**Category:** Network Forensics, Threat Hunting  
**Room Link:** [C2 Detection - Command & Carol](https://tryhackme.com/room/detecting-c2-with-rita-aoc2025-m9n2b5v8c1) 
**Status:** ✔ Completed  

---

## 🧭 Overview

After a long chain of attacks by King Malhare’s underlings, TBFC remains on high alert.  
This time, instead of reacting to an alert, **Sir Elfo** proposes proactive threat hunting using **network traffic analysis**.

The challenge:  
Analyze **PCAP files** to uncover **Command and Control (C2)** activity — efficiently.

The solution:  
➡️ Convert PCAPs into **Zeek logs**  
➡️ Analyze them with **RITA (Real Intelligence Threat Analytics)**

---

## 🎯 Learning Objectives

- Convert a **PCAP** file into **Zeek logs**
- Import Zeek logs into **RITA**
- Analyze RITA output to detect **C2 activity**
- Understand **Threat Modifiers** and connection metadata

---

## ✨ The Magic of RITA

**RITA (Real Intelligence Threat Analytics)** is an open-source framework developed by **Active Countermeasures**.

### What RITA Detects
- C2 beaconing
- DNS tunneling
- Long-lived connections
- Data exfiltration
- Suspicious TLS behavior
- Known malicious IPs/domains
- Rare or abnormal traffic patterns

RITA works by correlating:
- IP addresses
- Ports
- Timestamps
- Connection intervals
- DNS and TLS metadata

---

## 🧠 Why Zeek?

RITA **only accepts Zeek logs**, not raw PCAPs.

**Zeek** is a network security monitoring tool that:
- Observes traffic (not a firewall or IDS)
- Converts packets into structured logs
- Extracts metadata and artifacts

Zeek provides:
- Transaction data (HTTP, DNS, SSL, connections)
- Extracted content (files, certificates)

---

## 🔄 Converting PCAP to Zeek Logs

Start the VM and open a terminal.

List directories:
``bash
ls

You should see:
pcaps
zeek_logs

Convert a PCAP to Zeek logs:
zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat

Navigate to the output:
cd ~/zeek_logs/asyncrat && ls

Example logs created:
conn.log
dns.log
http.log
ssl.log
files.log
x509.log
notice.log

---
## 📥 Importing Logs into RITA

Import Zeek logs:
rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat

RITA parses:
conn.log
http.log
ssl.log
dns.log

---
## 📊 Viewing RITA Results

View analysis:
rita view asyncrat

The interface contains:
Search bar
Results pane
Details pane

---
## 🔎 Understanding RITA Output

Results Pane Columns:

Severity score
Source → Destination
Beacon likelihood
Connection duration
Subdomain count
Threat intel matches

Threat Modifiers Explained:

MIME/URI mismatch
Rare signature
Prevalence
First seen
Missing host header
Large outbound data
No direct connections

Connection Info Includes:

Connection count
Total bytes sent
Port / protocol / service

---
## 🚨 Investigating Indicators

Notable findings:
. sunshine-bizrate-inc-software.trycloudflare.com
. 91.134.150.150
VirusTotal confirms these as malicious.

Other red flags:

Long connection durations
Non-standard ports
Rare TLS signatures

---
## 🧪 RITA Challenge Analysis

Analyze:
~/pcaps/rita_challenge.pcap

Follow the same steps:

Convert PCAP → Zeek logs
Import into RITA
Analyze results

---
## 🏁 Answers

How many hosts communicate with malhare.net?
Follow the same steps:

Convert PCAP → Zeek logs

Import into RITA

Analyze results

🏁 Answers

How many hosts communicate with malhare.net?
6

Which Threat Modifier shows number of hosts?
prevalence

Highest number of connections to rabbithole.malhare.net?
40

Search filter for beacon score > 70% sorted by duration
dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc

Which port did 10.0.0.13 use?
80

---
## 🧠 Key Takeaways

PCAPs alone are noisy; analytics matter
RITA simplifies large-scale C2 detection
Threat hunting requires context, not just alerts
Even low-severity entries can be malicious

---
## ✅ Day 22 Completed

C2 infrastructure identified.
Threat hunting skills sharpened.
Ready for the next SOC-mas challenge.

---
## 🔜 Next Step

Proceed to Day 23 of Advent of Cyber 2025.
