# 🎄 Advent of Cyber 2025 — Day 9  
<img src="./images/day9-banner.png" width="900"/>

**Title:** Passwords - A Cracking Christmas                                                                                  
**Date Completed:** Dec 2025  
**Difficulty:** Easy–Medium  
**Category:** Crypto, Password Cracking, Forensics  
**Room Link:** [Passwords - A Cracking Christmas](https://tryhackme.com/room/attacks-on-ecrypted-files-aoc2025-asdfghj123)   
**Status:** ✔ Completed  

---

## 🧭 Overview  
Encrypted PDF and ZIP files labelled **“North Pole Asset List”** were discovered on TBFC servers. Sir Carrotbane suspects weak passwords protect them.  
Today’s task is to understand how password-based encryption works, why weak passwords fail, and how attackers use dictionary and mask/brute-force attacks to recover passwords and reveal file contents.

---

# 🧩 Task-by-Task Write-Up

---

## **📝 Task 1 — Encryption & Password Strength**
- Password-based encryption protects files (PDF, ZIP) by deriving keys from passwords.  
- Strength depends almost entirely on the password (length, complexity, randomness).  
- Different formats use different derivation methods (salts, iteration counts) — this affects crackability.

Key point: attackers target the **password**, not cryptanalysis of the algorithm.

---

## **🔎 Task 2 — Common Attack Methods**

### **Dictionary Attacks**
- Use wordlists (e.g., `rockyou.txt`) to try common passwords fast.  
- First step for most offline cracking tasks.

### **Mask / Brute-force Attacks**
- Mask attacks narrow search (e.g., `?l?l?l?d?d` = 3 letters + 2 digits).  
- Full brute-force tries every possible combination — exponential time.

### **Tooling**
- **PDF**: `pdfcrack`, `pdf2john.pl` + `john`
- **ZIP**: `fcrackzip`, `zip2john` + `john`
- **General/Advanced**: `john`, `hashcat` (GPU-accelerated)

Examples:
```
pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt
zip2john flag.zip > ziphash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt
```

---

## **⚡ Task 3 — Practical Cracking**
- Confirm file types with `file` (PDF vs ZIP) or a hex viewer.  
- Try a wordlist first — often a fast win.  
- If that fails, escalate to masks or incremental brute-force.  
- Monitor resource usage (CPU/GPU); cracking is resource-intensive.

Example outputs:
- `pdfcrack` reporting `'found user-password: 'XXXXXXXXXX'`  
- `john` showing cracked password and affected file `(flag.zip/flag.txt)`

---

## **🔎 Task 4 — Detection & Telemetry**
Offline cracking is noisy on endpoints (not network):

Detectable signals:
- Process creation for `john`, `hashcat`, `pdfcrack`, `fcrackzip`, `zip2john`, `pdf2john.pl`  
- Command-line flags: `--wordlist`, `--mask`, `zip2john`, `pdf2john`  
- Potfiles: `~/.john/john.pot`, `.hashcat/hashcat.potfile`  
- Heavy GPU/CPU usage (`nvidia-smi` shows long-running `hashcat` or `john` jobs)  
- Downloads of large wordlists (e.g., `rockyou.txt`)

Example detections:
- Sysmon process create rules for cracking binaries  
- Linux `auditctl` rules for monitoring `john`/`hashcat` execution  
- Sigma rule examples for Windows process creation

---

## **🛠 Response Playbook (Analyst Actions)**
1. Isolate suspicious host (or tag/suppress if lab).  
2. Triage artefacts: process list, memory dump, `nvidia-smi` snapshot, open files.  
3. Preserve working directories, wordlists, hash files, shell history.  
4. Search decrypted files for follow-on access or exfiltration.  
5. Determine intent (authorized vs unauthorized).  
6. Remediate: rotate keys/passwords, enforce MFA, clean infected systems.  
7. Educate and move cracking tools into approved sandboxes.

---

# 🏁 Final Answers / Flags

**Flag inside encrypted PDF:**  
```
THM{Cr4ck1ng_PDFs_1s_34$y}
```

**Flag inside encrypted ZIP file:**  
```
THM{Cr4ck1n6_z1p$_1s_34$yyyy}
```

---

# 🎯 Learning Objectives Achieved
- How password-based encryption protects files and why weak passwords fail.  
- Practical use of dictionary and mask attacks for PDFs and ZIPs.  
- Tools: `pdfcrack`, `fcrackzip`, `zip2john`, `pdf2john`, `john`, `hashcat`.  
- Detection opportunities on endpoints and in telemetry.  
- Response playbook for suspected cracking activity.

---

# 📘 What I Learned Today  
> “Encryption is only as strong as the password protecting it — offline cracking exploits human weakness, not cryptography.”

---

# 🔜 Next Step  
Proceed to **Day 10** of Advent of Cyber 2025.


