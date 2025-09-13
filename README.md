# SOC Honeypot and Splunk Lab

## Project Overview
This project simulates a **Security Operations Center (SOC) environment** by deploying a **Cowrie honeypot** on an Ubuntu VM and forwarding logs to **Splunk Enterprise** running on a Kali Linux VM.  
An attacker VM (Kali pre-built) was used to generate brute-force attempts using **Hydra**, and all events were captured and visualized in Splunk dashboards.

**Goal:** Learn how logs are ingested, monitored, and analyzed within a SOC-style environment..

---

## 🛠️ Tools & Technologies
- **Splunk Enterprise** (SIEM for log collection & dashboards)  
- **Splunk Universal Forwarder** (log forwarding from Ubuntu to Splunk)  
- **Cowrie Honeypot** (SSH/Telnet honeypot to simulate attacks)  
- **Hydra** (attack simulation with brute-force login attempts)  
- **Kali Linux & Ubuntu VMs** (multi-VM environment on VMware)  

---

## ⚙️ Lab Setup (High-Level)
1. **Splunk Enterprise VM (Kali)**  
   - Installed Splunk Enterprise.  
   - Configured receiving on port `9997`.  

2. **Ubuntu VM (Honeypot)**  
   - Installed and ran Cowrie.  
   - Installed Splunk Universal Forwarder.  
   - Configured forwarder to send logs (`cowrie.json` & `cowrie.log`) to Splunk.  

3. **Attacker VM (Kali pre-built)**  
   - Used **Hydra** to brute-force SSH on Cowrie honeypot (example):  
   ```bash
   hydra -l root -P /usr/share/wordlists/rockyou.txt -s 2222 ssh://<Ubuntu_IP> -t 4

4. Splunk Verification
   Example search to verify ingestion:
   index=main sourcetype=cowrie_json

---

## Dashboards & Detections (What I Built)
- Simple **timechart** of failed SSH login attempts.  
- Basic **event listing** of login attempts captured by Cowrie.  

*(Note: Advanced detections like top attacker IPs, common credentials, or malware downloads were not implemented in this lab, but could be added later.)*

---

## Repo Contents

-README.md → this documentation

-SOC_HONEYPOT_SPLUNK_LAB_SS.pdf → screenshots and evidence

---

## Resume Bullets

-Built a multi-VM SOC lab: deployed Splunk Enterprise and Cowrie honeypot; configured Splunk Universal Forwarder to ingest Cowrie JSON logs.

-Verified ingestion in Splunk using searches (index=main sourcetype=cowrie_json).

-Simulated brute-force attacks with Hydra to test detection pipeline.

---

## Notes

-Before making the repo public, replace or remove any real home IPs (e.g., 192.168.x.x) or admin passwords.

-Do not upload VM images or private keys. Screenshots and config snippets are enough to prove the work.