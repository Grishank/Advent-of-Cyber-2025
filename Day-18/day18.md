# 🎄 Advent of Cyber 2025 — Day 18  
<img src="./images/day18-banner.png" width="900"/>

**Title:** Obfuscation - The Egg Shell File  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Malware Analysis, Obfuscation, Blue Team  
**Room Link:** [Obfuscation - The Egg Shell File](https://tryhackme.com/room/obfuscation-aoc2025-e5r8t2y6u9)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

WareVille has not felt right since the wormhole appeared. TBFC systems are behaving erratically, dashboards are spiking, and SOC alerts are firing nonstop.

Among the chaos, McSkidy noticed a suspicious email impersonating **northpole-hr**, filled with carrot emojis. The strange part?  
There is **no North Pole HR department** — TBFC’s HR operates from the **South Pole**.

Further investigation revealed a tiny **PowerShell file** downloaded from the email. The script appeared to contain random gibberish, indicating the use of **obfuscation** to hide malicious intent.

The objective was to understand obfuscation techniques, safely deobfuscate the script, and recover the attacker’s hidden data.

---

## 🎯 Learning Objectives

- Understand **obfuscation**, why it is used, and where it appears  
- Learn the difference between **encoding, encryption, and obfuscation**  
- Identify common obfuscation techniques  
- Use **CyberChef** to safely recover plaintext  

---

## 🧠 Understanding the Gibberish

**Obfuscation** is the practice of intentionally making data difficult to read or analyze.  
Attackers use it to evade detection and slow down investigations.

Example:  
If security tools block the word `bandit yeti`, attackers may apply simple ciphers like **ROT1**.

ROT1 shifts each character forward by one letter:
carrot coins go brr
↓
dbsspu dpjot hp css

ROT13 increases complexity by shifting letters forward by 13 positions.

---

## 🌍 Obfuscation in the Real World

In real malware, attackers often use more complex techniques such as **XOR**.

XOR works by:
- Converting characters into bytes  
- Applying a bitwise XOR operation using a key  
- Producing unreadable or symbolic output  

This is not practical to reverse manually, but tools like **CyberChef** make it manageable.

---

## 🧰 Obfuscating Data with XOR (CyberChef)

Steps:
1. Open CyberChef
2. Enter the input:
   
carrot supremacy
3. Add the **XOR** operation
4. Set the key to:
a
5. Ensure the key format is **HEX**
6. Click **BAKE!**

Resulting obfuscated output:
ikxxe~*yzxogkis!

---

## 🔍 Detecting Obfuscation Patterns

Common visual clues:

- **ROT1**  
  Letters appear one position off; spaces unchanged  

- **ROT13**  
  Common words look transformed (e.g., `the` → `gur`)  

- **Base64**  
  Long alphanumeric strings, may end in `=` or `==`  

- **XOR**  
  Appears random, same length as input, repeating patterns may appear  

Once identified, the reverse operation can be applied using CyberChef.

---

## 🪄 Unfamiliar Patterns — CyberChef Magic

If unsure which technique was used:
- Add the **Magic** operation in CyberChef
- Enable **Intensive mode**
- Review multiple output possibilities
- Choose the result that makes logical sense

Magic provides hints but may not fully solve layered obfuscation.

---

## 🧩 Layered Obfuscation

Attackers often combine multiple techniques.

Example:
- Compress with **gzip**
- XOR with key `x`
- Encode with **Base64**

Resulting obfuscated string:
xxxxxxxxxxxxxxxxxxxxxxxxxx

To reverse:
1. From Base64  
2. XOR with key  
3. Decompress gzip  

---

## 🐣 Unwrapping the Easter Egg

McSkidy extracted a suspicious PowerShell script from the email:
SantaStealer.ps1

The script was analyzed in an **isolated VM**.

Steps:
1. Open `SantaStealer.ps1` in Visual Studio  
2. Navigate to the **Start here** section  
3. Follow the instructions in the comments  
4. Save the script  
5. Open PowerShell and run:

``powershell
cd .\Desktop\
.\SantaStealer.ps1
This revealed the first flag after deobfuscating the C2 URL.
.
---
## 🔐 Second Challenge — Obfuscating the API Key

The script contained Part 2 instructions:
Obfuscate the attacker’s API key using XOR
Follow the comments in the script

Run the script again

This produced the final flag.
---

## 🏁 Final Answers / Flags

First Flag:
THM{C2_De0bfuscation_29838}

Second Flag:
THM{API_Obfusc4tion_ftw_0283}
---

## 🎯 Learning Objectives Achieved

Understood obfuscation and its purpose
Differentiated encoding, encryption, and obfuscation
Identified common obfuscation techniques
Used CyberChef to safely recover plaintext
Analyzed and modified malicious PowerShell code

---
## 📘 What I Learned Today
“Obfuscation doesn’t stop analysis — it just buys attackers time.”

---
## 🔜 Next Step
Proceed to Day 19 of Advent of Cyber 2025.
---
