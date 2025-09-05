# franklin_portfolio
This project presents a real-world incident response case study where I analyzed malicious file upload activity, identified Command &amp; Control (C2) behavior, and performed behavioral malware analysis using network forensics and sandbox investigation tools. All sensitive client identifiers have been anonymized.
Skills demonstrated: Packet analysis, malware behavior analysis, threat hunting, sandboxing, PowerShell decoding, MITRE ATT&CK mapping, VirusTotal IOC review.

Title: Malicious File Upload & C2 Beacon Detection – FinanceTech Corp

📝 Executive Summary

During a proactive threat hunting and incident response exercise for FinanceTech Corp, I analyzed suspicious file upload traffic originating from an internal workstation. The investigation revealed a macro-enabled Word document embedded in a ZIP file uploaded to an external server.

Sandbox analysis showed the use of obfuscated PowerShell and outbound communication to a Command & Control (C2) server. The behavior suggested automated malware generation, likely from Metasploit's msfvenom.

🔍 Objective

Detect and investigate a suspicious outbound file upload, identify potential malware activity, uncover any external C2 communication, and assess threat techniques using MITRE ATT&CK mapping.

🧠 Key Skills Demonstrated
Area	Description
🧪 Packet Analysis	Used Wireshark to extract suspicious file upload and reconstruct HTTP payload
🔒 Sandbox Analysis	Used ANY.RUN to detonate and trace macro execution, PowerShell behavior, and C2 activity
🔁 Threat Hunting	Traced execution chain from Word macro to obfuscated PowerShell to beaconing
🔗 MITRE ATT&CK	Mapped TTPs such as PowerShell execution (T1059.001), Macro abuse (T1566.001), and C2 over HTTPS (T1071.001)
🧬 Malware Attribution	Identified behavior consistent with known offensive security tools (msfvenom)
🧾 IOC Reporting	Documented IOCs including MD5 hashes, C2 domains, and IP addresses
🔍 Investigation Summary
Suspicious Upload Behavior

Source IP: 192.168.10.111 (internal asset)

Destination IP: 178.128.25.67 (external server)

Filename: Resume-2021.zip

Embedded File: Resume John Doe.doc

MD5 Hash: 9EAE9BD90ED69A3ABBBACEA573A233B0

Tools Used
Tool	Purpose
Wireshark	Traffic inspection, file extraction, stream following
ANY.RUN	Sandbox execution and process tracing
VirusTotal	Threat classification and hash lookup
PowerShell	Base64 decoding
MITRE ATT&CK	TTP mapping
🧪 Technical Walkthrough
🛰️ Q1–Q4: Traffic Inspection & File Extraction

Used Wireshark to filter http.request.method == "POST"

Exported Resume-2021.zip from packet stream

Hash generated: MD5 9EAE9BD90ED69A3ABBBACEA573A233B0

🧾 Q5: File Content Review

Analyzed Word doc in sandbox → contained education history: B.S. Astronomy, Computer Science, 2019

🌐 Q6–Q7: C2 Discovery

Macro → Obfuscated PowerShell → Connected to:

nexusrules.officeapps.live.com
IP: 52.111.229.19


Traffic pattern mimicked Microsoft, but verified as malicious staging server.

💥 Q8: Malware Execution Chain
Macro → powershell.exe -nop -sta -w 1 -enc <base64> → conhost.exe → C2 Communication


Indicators of fileless execution.

Used ANY.RUN process tree to visualize command sequence.

🧰 Q9: Malware Generator Attribution

Behavior consistent with Metasploit (msfvenom) payload:

Base64-encoded PowerShell

Staged execution

Meterpreter-style C2

🧾 VirusTotal Findings

Hash: 9EAE9BD90ED69A3ABBBACEA573A233B0

Detection: 31/60 engines flagged

Tags:

Trojan-Downloader.PowerShell.Agent

VB.Trojan.Valyria

Macro.Agent

Metasploit Payload

🧩 MITRE ATT&CK Techniques
Technique ID	Description
T1059.001	PowerShell Execution
T1566.001	Spearphishing Attachment
T1055	Process Injection
T1071.001	Application Layer Protocol: HTTPS (C2)
T1204.002	User Execution: Malicious Document
📍 Indicators of Compromise (IOCs)
Source IP:         192.168.10.111
Destination IP:    178.128.25.67
File Name:         Resume-2021.zip
MD5:               9EAE9BD90ED69A3ABBBACEA573A233B0
C2 Domain:         nexusrules.officeapps.live.com
C2 IP:             52.111.229.19

🧠 Key Takeaways

File uploads to unknown hosts over HTTP should be monitored.

Macro-enabled documents remain a popular initial access vector.

Obfuscated PowerShell is often a red flag for post-exploitation.

Proper use of sandboxing tools like ANY.RUN can quickly reveal hidden behavior.

C2 traffic disguised as trusted services (like "officeapps.live.com") is common and should be validated.

📂 Repository Content Suggestions

/pcap-analysis/ — Screenshots of Wireshark filters and file extraction

/sandbox-analysis/ — Screenshots of ANY.RUN execution (process tree, network logs, DNS queries)

/ioc-report/ — Summary of IOCs and MITRE mappings

/README.md — Full report for recruiters/interviewers

📢 Final Pitch (GitHub, Resume, or Interview)

This project highlights my hands-on experience in incident response—from network packet analysis to dynamic malware analysis, TTP mapping, and actionable IOC generation. It reflects how I approach real-world investigations, enabling security teams to identify, confirm, and respond to threats effectively.
