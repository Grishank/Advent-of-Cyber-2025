# 🎄 Advent of Cyber 2025 — Day 16  
<img src="./images/day16-banner.png" width="900"/>

**Title:** Forensics - Registry Furensics 
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Digital Forensics, Windows Internals, Blue Team  
**Room Link:** [Forensics - Registry Furensics](https://tryhackme.com/room/registry-forensics-aoc2025-h6k9j2l5p8)            **Status:** ✔ Completed  

---

## 🧭 Overview  

TBFC is under attack. Systems across the organisation are behaving abnormally, and the absence of the lead defender **McSkidy** is being felt deeply.  

One of the most critical systems, **dispatch-srv01**, which coordinates drone-based gift deliveries during SOCMAS, was compromised by **King Malhare’s bandit bunnies**.

To uncover the attack, TBFC’s defenders split into specialised forensic teams.  
While other teams investigated logs, memory dumps, and file systems, **my task focused on Registry Forensics** — analysing the Windows Registry of the compromised server.

---

## 🎯 Learning Objectives

- Understand what the **Windows Registry** is and what it stores  
- Learn about **Registry Hives and Root Keys**  
- Analyze Registry data using **Registry Editor**  
- Perform **offline Registry Forensics** using **Registry Explorer**

---

## 🧠 Windows Registry Explained

Just like the human brain stores habits, preferences, and past actions,  
the **Windows Registry** stores all configuration information required for the OS to function.

The registry includes:
- System configuration  
- Installed software  
- User preferences  
- Startup programs  
- Security settings  

Unlike a human brain, the registry is **not stored in a single location**.  
It is divided into multiple files called **Registry Hives**.

---

## 🗂️ Registry Hives

| Hive Name | Contains | Location |
|---------|---------|---------|
| SYSTEM | Services, boot config, drivers, hardware | `C:\Windows\System32\config\SYSTEM` |
| SECURITY | Local security & audit policies | `C:\Windows\System32\config\SECURITY` |
| SOFTWARE | Installed programs, OS info, autostarts | `C:\Windows\System32\config\SOFTWARE` |
| SAM | User accounts, password hashes, groups | `C:\Windows\System32\config\SAM` |
| NTUSER.DAT | User activity, preferences, autostarts | `C:\Users\username\NTUSER.DAT` |
| USRCLASS.DAT | Shellbags, jump lists | `C:\Users\username\AppData\Local\Microsoft\Windows\USRCLASS.DAT` |

> Note: Each hive stores far more data than the examples listed above.

---

## 🗝️ Registry Hives vs Root Keys

Registry Hives are mapped into **Root Keys** in the Registry Editor.

| Hive on Disk | Registry Editor Location |
|-------------|--------------------------|
| SYSTEM | `HKEY_LOCAL_MACHINE\SYSTEM` |
| SECURITY | `HKEY_LOCAL_MACHINE\SECURITY` |
| SOFTWARE | `HKEY_LOCAL_MACHINE\SOFTWARE` |
| SAM | `HKEY_LOCAL_MACHINE\SAM` |
| NTUSER.DAT | `HKEY_USERS\<SID>` and `HKEY_CURRENT_USER` |
| USRCLASS.DAT | `HKEY_USERS\<SID>\Software\Classes` |

Other keys like **HKCR** and **HKCC** are dynamically populated and do not map to standalone hive files.

---

## 🔍 Extracting Information from the Registry

### Example 1 — Connected USB Devices

Path:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR

This key stores:
- USB make & model  
- Device identifiers  
- Unique connected devices  

---

### Example 2 — Programs Run via Win + R

Path:
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU

This key shows:
- Commands executed using the **Run dialog**
- User execution history

---

## 🧪 Registry Forensics

**Registry Forensics** involves extracting evidence from registry hives to reconstruct attacker activity.

In real investigations, analysts correlate:
- Registry artefacts  
- Event logs  
- File system data  
- Memory artefacts  

to build a complete timeline.

---

## 🧭 High-Value Registry Keys for Forensics

| Registry Key | Importance |
|-------------|------------|
| `HKCU\...\UserAssist` | Recently executed GUI programs |
| `HKCU\...\TypedPaths` | Paths typed in Explorer |
| `HKLM\...\App Paths` | Application execution paths |
| `HKCU\...\WordWheelQuery` | Search terms typed |
| `HKLM\...\Run` | Startup programs |
| `HKCU\...\RecentDocs` | Recently accessed files |
| `HKLM\SYSTEM\...\ComputerName` | Hostname |
| `HKLM\SOFTWARE\...\Uninstall` | Installed programs |

---

## 🛠️ Why Registry Explorer?

- Registry Editor **cannot open offline hives**
- Some values appear as **binary and unreadable**
- Live system analysis risks **modifying evidence**

**Registry Explorer**:
- Parses binary values  
- Loads offline hives safely  
- Replays transaction logs  
- Ideal for forensic investigations  

---

## 🔬 Practical — Registry Analysis

### Step 1: Launch Registry Explorer
Open **Registry Explorer** from the taskbar on the target machine.

---

### Step 2: Load Offline Registry Hives

1. Click **File → Load hive**
2. Navigate to:

C:\Users\Administrator\Desktop\Registry Hives
3. Select a hive (e.g., SYSTEM)
4. Hold **SHIFT** and click **Open** to load transaction logs

This ensures a clean and consistent hive state.

Repeat for all required hives.

---

### Step 3: Investigate Registry Keys

To find the computer name:

Path:
ROOT\ControlSet001\Control\ComputerName\ComputerName

Or search for:
ComputerName

Value found:
DISPATCH-SRV01

This confirms the hostname of the compromised system.

---

## 🧠 Investigation Context

- Abnormal activity began on **21st October, 2025**
- Registry artefacts help establish:
  - Persistence mechanisms  
  - User activity  
  - System configuration changes  

> Tip: The Registry Forensics table is extremely useful during analysis.

---

## 🎯 Learning Objectives Achieved

- Understood Windows Registry internals  
- Learned registry hive structure and mapping  
- Performed offline registry analysis  
- Used Registry Explorer for forensic investigation  
- Extracted host-specific evidence safely  

---

## 📘 What I Learned Today

> “The registry remembers everything — even when attackers think they’ve cleaned up.”

---

## 🔜 Next Step

Proceed to **Day 17** of Advent of Cyber 2025.

