# 🎄 Advent of Cyber 2025 — Day 19  
<img src="./images/day19-banner.png" width="900"/>

**Title:** ICS/Modbus - Claus for Concern  
**Date Completed:** Dec 2025  
**Difficulty:** Hard  
**Category:** ICS Security, SCADA, Modbus, Blue Team  
**Room Link:** [ICS/Modbus - Claus for Concern](https://tryhackme.com/room/ICS-modbus-aoc2025-g3m6n9b1v4)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

WareVille is in chaos. What should have been the busiest shipping day before SOC-mas has turned into a disaster.  
TBFC’s drone delivery fleet is operational, dashboards look normal, and success rates appear high — yet citizens keep receiving **chocolate eggs instead of Christmas gifts**.

A brief taunt flashes on the monitoring screen:

---
## 🐰 EGGSPLOIT v6.66 - Property of HopSec Island 🐰
"Why should Christmas have all the fun?" - King Malhare

The attack is subtle and dangerous:
- Sensor data falsified
- Inventory manipulation
- Audit logs disabled
- Trap mechanisms armed

This is not IT — this is **ICS compromise**.

---

## 🎯 Learning Objectives

- Understand how **SCADA systems** monitor industrial processes  
- Learn how **PLCs** control real-world automation  
- Understand the **Modbus protocol** and its weaknesses  
- Identify compromised configurations in ICS environments  
- Perform **safe remediation** without triggering traps  
- Understand protection mechanisms and trap logic  

---

## 🏭 What is SCADA?

SCADA (Supervisory Control and Data Acquisition) systems are the **command centres** of industrial operations.

They:
- Monitor physical processes
- Collect sensor data
- Allow operators to control machinery
- Store historical data for analysis

TBFC uses SCADA to manage:
- Drone loading
- Inventory selection
- Delivery routing
- CCTV monitoring
- Safety mechanisms

---

## 🧩 Components of a SCADA System

1. **Sensors & Actuators**  
   - Sensors measure weight, position, status  
   - Actuators move conveyor belts, robotic arms  

2. **PLCs (Programmable Logic Controllers)**  
   - Execute automation logic in real time  
   - Make decisions based on sensor input  

3. **Monitoring Systems**  
   - Dashboards, alarms, CCTV feeds  

4. **Historians**  
   - Databases storing operational data  

---

## 🎯 Why SCADA Systems Are Targeted

- Legacy software
- Default credentials
- Designed for reliability, not security
- Control physical processes
- Often connected to corporate networks
- Protocols like Modbus **lack authentication**

In 2024, **FrostyGoop**, the first ICS malware, demonstrated real-world Modbus attacks.

King Malhare used the same approach.

---

## 🔌 What is Modbus?

Modbus is an industrial communication protocol created in 1979.

It works via **simple request-response**:
Client: Read register 0
PLC: Register 0 = 1

Security flaws:
- No authentication
- No encryption
- No authorization
- Anyone on the network can read/write values

Default Modbus TCP port:
502

---

## 🧠 Modbus Data Types

| Type | Purpose | Writable | Example |
|----|--------|----------|--------|
| Coils | Boolean outputs | Yes | Alarm on/off |
| Discrete Inputs | Boolean inputs | No | Sensor state |
| Holding Registers | Numeric outputs | Yes | Mode selection |
| Input Registers | Numeric inputs | No | Temperature |

---

## 📄 TBFC Register Map (From the Note)

### Holding Registers
- **HR0** — Package Type  
  - 0 = Christmas Gifts  
  - 1 = Chocolate Eggs  
  - 2 = Easter Baskets  

- **HR1** — Delivery Zone  
  - 1–9 = Normal  
  - 10 = Ocean dump  

- **HR4** — System Signature  
  - 666 = Eggsploit  

### Coils
- **C10** — Inventory Verification  
- **C11** — Protection / Trap  
- **C12** — Emergency Dump  
- **C13** — Audit Logging  
- **C14** — Christmas Restored  
- **C15** — Self-Destruct  

⚠️ **CRITICAL WARNING**  
Never change HR0 while C11 = True

---

## 🔍 Initial Reconnaissance

### Nmap Scan
nmap -sV -p 22,80,502 MACHINE_IP

Key services:
- Port 80 — CCTV Web Interface
- Port 502 — Modbus TCP

---

## 🎥 Visual Confirmation (CCTV)

Access:
http://MACHINE_IP

Observed:
- Chocolate eggs on conveyor
- Easter packaging
- Drones loading wrong items
- Status: **Compromised**

This confirms a **logic manipulation attack**, not system failure.

---

## 🐍 Modbus Recon with PyModbus

### Connect to PLC
``python
from pymodbus.client import ModbusTcpClient

client = ModbusTcpClient('MACHINE_IP', port=502)
client.connect()

Read Holding Registers
client.read_holding_registers(0, 1)

Results:
HR0 = 1  (Chocolate Eggs)
HR1 = 5  (Normal Zone)
HR4 = 666 (Eggsploit signature)

Read Coils
client.read_coils(10, 6)

Findings:

C10 = False (Inventory check disabled)
C11 = True (Trap armed)
C13 = False (Logging disabled)
C15 = False (Self-destruct not yet armed)

---
## 🚨 Understanding the Trap

If HR0 is changed while C11 is True:
C15 arms
30-second countdown
C12 activates
Inventory dumped to ocean
Challenge reset

---
## 📜 Reconnaissance Script

A full reconnaissance script was written to safely enumerate:
Registers
Coils
Threat state

Result:
Eggsploit detected
Trap active
Inventory verification disabled
Audit logging disabled
Remediation required

---
## 🛠️ Safe Remediation Strategy

Correct order:
Disable protection (C11)
Set HR0 = 0 (Christmas gifts)
Enable inventory verification (C10)
Enable audit logging (C13)
Verify C15 never armed

---
## 🎄 Restoration Script Outcome

Execution result:
SUCCESS - CHRISTMAS IS SAVED

Drones now deliver Christmas presents, not eggs.

---
## 🏁 Final Flag
THM{eGgMas0V3r}

---
## 🧠 Post-Incident Analysis

King Malhare:
Used unauthenticated Modbus
Disabled safety controls
Weaponized protection mechanisms
Left a signature (666)
The maintenance note prevented disaster.

---
## 🎯 Learning Objectives Achieved

Understood SCADA & PLC operations
Identified Modbus exploitation
Safely remediated ICS compromise
Avoided trap mechanisms
Restored physical operations

---
## 📘 What I Learned Today

“In ICS, one wrong command can destroy more than data.”

---
## 🔜 Next Step

Proceed to Day 20 of Advent of Cyber 2025.
---

