# 🔍 The Greenholt Phish – Email Forensics & Threat Intelligence Analysis

[![Platform](https://img.shields.io/badge/Platform-TryHackMe-black?style=flat&logo=tryhackme)](https://tryhackme.com)
[![Path](https://img.shields.io/badge/Path-SOC%20Level%201-blue?style=flat)](https://tryhackme.com/path/outline/soclevel1)
[![Topic](https://img.shields.io/badge/Topic-Phishing%20Forensics-red?style=flat)](https://tryhackme.com)
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange?style=flat)](https://tryhackme.com/room/phishingemails5fgjlzxc)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat)]()

Real-world phishing email investigation from TryHackMe SOC Level 1 path.  
A Sales Executive at Greenholt PLC received a suspicious email claiming a large transfer had been made to his account. The email used a generic greeting, unexpected tone, and contained an unrequested attachment. Forwarded to SOC for triage.

Performed full email forensics: header analysis, SPF/DMARC validation, originating IP ownership lookup, attachment metadata extraction, hash lookup on VirusTotal, and threat intelligence enrichment via AbuseIPDB.

Demonstrates Tier-1 SOC analyst capabilities: email source inspection, authentication record validation, IOC enrichment, and structured incident reporting.

## 📌 Quick Summary
**Room**: The Greenholt Phish  
**Scenario**: Suspicious customer email claiming unauthorized transfer + unexpected attachment  
**Key Deliverables**:
- Extracted Transfer Reference Number, sender details, originating IP, Reply-To mismatch
- Validated SPF & DMARC records for Return-Path domain
- Identified attachment name, SHA256 hash, file size, true file extension
- Enriched IOCs with VirusTotal and AbuseIPDB lookups
- Documented full forensic workflow and defensive takeaways

## 🎯 Objectives & Achievements
- Analyzed raw .eml file in Thunderbird
- Extracted key fields: Subject, From, Reply-To, Originating IP, attachment metadata
- Performed DNS lookups for SPF & DMARC records on Return-Path domain
- Computed SHA256 hash and verified file type (true extension hidden)
- Enriched originating IP with AbuseIPDB threat intelligence
- Scanned attachment on VirusTotal for known malicious signatures
- Mapped behavior to MITRE ATT&CK Initial Access (T1566 Phishing)

## 🛠 Tools & Workflow
- Thunderbird (open & inspect .eml file)
- Wireshark / Network tools (not required, but context for SMTP if extended)
- VirusTotal (attachment hash lookup & reputation check)
- SPF Surveyor / DMARC Record Analyzer (authentication record validation)
- AbuseIPDB (originating IP threat intelligence)
- CyberChef / online base64/hex tools
- Command line (sha256sum / file command for hash & type verification)

## 🔎 Detailed Analysis & Findings

### Email Metadata & Spoofing Indicators
- **Transfer Reference Number** (from Subject): [09674321]
- **From name & email**: [Mr. James Jackson,info@mutawamarine.com]
- **Reply-To address** (where replies would actually go): [info.mutawamarine@mail.com]
- **Originating IP**: [192.119.71.157]  
  Owner (AbuseIPDB): [Hostwinds LLC]

### SPF & DMARC Validation (Return-Path domain)
- SPF record: [v=spf1 include:spf.protection.outlook.com -all]
- DMARC record: [v=DMARC1; p=quarantine; fo=1]

### Attachment Analysis
- Filename as shown: [SWT_#09674321____PDF__.CAB]
- True file extension: [RAR]
- SHA256 hash: [2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f]
- File size: [400.26 KB]

### IOC Enrichment
- Originating IP reputation checked via AbuseIPDB
- Attachment hash submitted to VirusTotal for known malware signatures

## 🔎 Evidence – Wireshark SMTP & Email Forensics

### Malicious Email – Full View
<img src="https://i.imgur.com/n9hlpTt.png" width="850" alt="Full view of the malicious phishing email">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">Overview of the malicious email – visible subject, sender, and attachment lure</figcaption>

### Email Source Code – Raw Headers & Body
<img src="https://i.imgur.com/w0MVguL.png" width="850" alt="Raw source code of the phishing email">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">Raw email source – full headers (From, Reply-To, Received chain) and body inspection</figcaption>

### Attachment Filename
<img src="https://i.imgur.com/1oo4yK4.png" width="850" alt="Attachment filename displayed in email">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">Displayed attachment filename – initial lure name shown to recipient</figcaption>

### AbuseIPDB – Originating IP Owner Lookup
<img src="https://i.imgur.com/QP5iLou.png" width="850" alt="AbuseIPDB lookup – owner of the originating IP">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">AbuseIPDB enrichment – ownership and reputation of the originating IP address</figcaption>

### File Size on Desktop
<img src="https://i.imgur.com/ixXVYPM.png" width="850" alt="File size of the downloaded attachment on desktop">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">Attachment file size verification directly on the desktop</figcaption>

### SHA256 Hash via Terminal
<img src="https://i.imgur.com/7u7S4b3.png" width="850" alt="Terminal output showing sha256sum of the attachment">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">Command-line SHA256 hash computation of the downloaded attachment file</figcaption>

### DMARC Record – Return-Path Domain
<img src="https://i.imgur.com/uRJFXAB.png" width="850" alt="DMARC record lookup for Return-Path domain">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">DMARC record validation – Return-Path domain authentication policy</figcaption>

### SPF Record Survey – Return-Path Domain
<img src="https://i.imgur.com/yLcGGaI.png" width="850" alt="SPF record survey for Return-Path domain">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">SPF record lookup – authorized senders for Return-Path domain</figcaption>

### VirusTotal – Attachment File Size Confirmation
<img src="https://i.imgur.com/WlnUnBd.png" width="850" alt="VirusTotal scan showing attachment file size">
<figcaption style="font-size:0.9em; color:#666; text-align:center;">VirusTotal analysis – confirmed file size of the submitted attachment</figcaption>

### VirusTotal – Actual File Extension Detection
<img width="1366" height="726" alt="image" src="https://github.com/user-attachments/assets/371eba14-55c2-43bd-829f-8730be4bfac5" />
VirusTotal results – true file extension revealed (hidden executable behind displayed name)</figcaption>

## 🧠 MITRE ATT&CK Mapping

| Tactic          | Technique                          | ID          | Observed Behavior                      |
|-----------------|------------------------------------|-------------|----------------------------------------|
| Initial Access  | Phishing                           | T1566       | Malicious email with attachment        |
| Initial Access  | Spearphishing Attachment           | T1566.001   | Unexpected attachment with hidden extension |
| Credential Access | Phishing for Information          | T1598       | Attempted credential harvesting lure   |
| Defense Evasion | Masquerading                       | T1036       | Spoofed sender & trusted customer mimicry |

## 🛡 Defensive Recommendations

### Technical Controls
- Strict DMARC p=reject + SPF/DKIM alignment on all domains
- Secure Email Gateway (SEG) or Microsoft Defender for Office 365 for impersonation & attachment scanning
- Time-of-click link rewriting & attachment detonation/sandboxing
- Block legacy SMTP (port 25) & enforce STARTTLS/SMTPS

### Detection Rules
- SIEM alerts on mismatched From/Reply-To domains
- Monitor for generic greetings + urgent transfer claims
- Endpoint rules: block execution of .scr, .zip with executables

### Human Layer
- External sender banners & suspicious attachment warnings
- One-click phishing reporting add-ins
- Regular phishing simulations targeting finance/transfer lures

These controls significantly reduce business email compromise (BEC) and attachment-based phishing success rates.

## 📌 Key Skills Demonstrated
- Manual .eml file forensics in Thunderbird
- SPF & DMARC record validation
- IP reputation enrichment (AbuseIPDB)
- Attachment hash lookup & file type verification (VirusTotal)
- IOC defanging & structured SOC reporting
- MITRE ATT&CK application to real phishing incidents

Solid Tier-1 phishing triage & threat intelligence enrichment capability.

Feel free to fork or star – open to discussions on BEC detection!

MIT License – see the [LICENSE](LICENSE) file for details.
