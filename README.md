# 🛡️ End-to-End SOC Lab: Attack Simulation, Detection, Mitigation & SIEM Monitoring📌 

## 📌 Executive Summary
This project demonstrates a complete Security Operations Center (SOC) workflow in a controlled virtualized lab environment. The objective was to simulate real-world cyber attacks, detect malicious activity through log analysis, apply mitigation strategies, and validate security improvements using centralized monitoring.

The lab successfully detected SSH brute-force attempts, anonymous FTP exploitation, SMB enumeration, and Windows brute-force attacks, while implementing defensive controls and integrating logs into a SIEM platform for enterprise-style monitoring.

## 🖥️ Lab Architecture

The environment was built using VirtualBox to simulate a segmented corporate LAN.

### 🔹 Systems Deployed

Kali Linux – Attacker + SIEM Access

Ubuntu Server – Web & SSH Target

Windows 10 – User Endpoint Target

OPNsense – Firewall & Network Gateway

Network segmentation was implemented using an isolated internal network with WAN/LAN separation through OPNsense.

Note: Large ISO files are intentionally excluded from this repository due to GitHub size limitations. The lab can be recreated using official Kali, Ubuntu, Windows, and OPNsense images.

🛠️ Tools & Technologies

VirtualBox (Virtualization)

OPNsense (Firewall & Traffic Logging)

Nmap (Network Discovery & Enumeration)

OpenVAS (Vulnerability Assessment)

Hydra (Brute-Force Attack Simulation)

Enum4linux (SMB Enumeration)

Sysmon (Windows Endpoint Monitoring)

Windows Event Viewer (Security Logs)

Linux Authentication Logs (/var/log/auth.log)

Splunk Enterprise / Splunk Cloud (Centralized SIEM Monitoring via Kali)

📍 Project Phases
🔎 Phase 1: Visibility & Asset Discovery

Verified IP addressing scheme

Configured WAN/LAN segmentation in OPNsense

Performed Nmap host discovery and service scans

Documented exposed services across systems

Created baseline network topology

Outcome: Achieved full visibility of internal assets and attack surface.

🔐 Phase 2: Baseline Security & Logging

Enabled firewall logging in OPNsense

Verified LAN-to-WAN connectivity

Configured static IP addressing

Implemented Sysmon (Event ID 1 – Process Creation)

Established normal traffic baseline

Outcome: Confirmed logging visibility before attack simulation.

🧪 Phase 3: Vulnerability Assessment
Ubuntu Findings:

Anonymous FTP Login (Medium)

FTP Cleartext Transmission (Medium)

TCP Timestamp Disclosure (Low)

ICMP Timestamp Disclosure (Low)

Windows Findings:

DCE/RPC Service Enumeration Exposure (Medium)

ICMP Timestamp Disclosure (Low)

OpenVAS scans validated exposed services and misconfigurations.

Outcome: Identified and documented security weaknesses for remediation.

🚨 Phase 4: Incident Simulation & Response
🔹 Attacks Simulated

SSH brute-force attack using Hydra

Anonymous FTP exploitation

SMB enumeration via Enum4linux

SMB brute-force attack on Windows Administrator

🔹 Detection Evidence

/var/log/auth.log (Linux authentication failures)

/var/log/vsftpd.log (Anonymous FTP login tracking)

Windows Event ID 4625 (Failed Logon)

Sysmon Event ID 1 (Process Creation Monitoring)

OPNsense firewall logs

🔹 Mitigation

Ubuntu:

Deployed Fail2Ban

Configured UFW rate limiting

Restricted SMB access

Hardened exposed services

Windows:

Documented remediation plan:

SMB firewall restrictions

Account lockout policy

Strong password enforcement

Advanced auditing

Patch management

Outcome: Validated attack detection, applied mitigation, and confirmed improved security posture.

📊 Phase 5: SIEM Integration & Advanced Monitoring
🔹 Log Ingestion

Installed Splunk Forwarder on Ubuntu and Windows

Manually configured Windows log ingestion via inputs.conf

Added SplunkForwarder to Event Log Readers group

Monitored:

/var/log/auth.log

/var/log/syslog

Windows Security & System logs

🔹 Detection Queries

Brute-Force Detection:

index=* host="DESKTOP-QKR30H3" EventCode=4625

Successful Logins:

index=* host="DESKTOP-QKR30H3" EventCode=4624

Privilege Escalation Monitoring:

index=* host="DESKTOP-QKR30H3" EventCode=4732

Indexed Events:

1,692 authentication events

3,714 system events

Outcome: Achieved centralized SOC-style log monitoring and threat visibility.

📊 Risk Summary
Vulnerability	Severity	Remediation Status
Anonymous FTP Login	Medium	Mitigated
FTP Cleartext Login	Medium	Mitigated
SMB Enumeration Exposure	Medium	Recommended Mitigation
ICMP Timestamp Disclosure	Low	Accepted Risk
🎯 Key Learning Outcomes

Practical SOC workflow implementation

Log correlation across Linux, Windows, and Firewall systems

Brute-force detection and mitigation strategies

Vulnerability assessment and risk evaluation

Endpoint monitoring using Sysmon

SIEM-based detection engineering

Incident lifecycle validation
