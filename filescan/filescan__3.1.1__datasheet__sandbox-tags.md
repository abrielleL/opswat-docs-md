<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/sandbox-tags -->

# Aether Tags

Tags are automatically generated based on the sample's analysis, providing a concise summary of key findings.

Tags are color-coded based on their severity context, with common colors like mediatype, high risk or confirmed thread, and no threat detected or low risk.

Some tags are dynamically derived from sandbox components or external sources, including:

- Threat indicators,
- YARA rules,
- Malware family attribution from [supported configuration extractors](metadefender-sandbox/2.1.0/datasheet/supported-malwares-for-config-extraction)
- CVE identifiers related to vulnerabilities,
- MISP Galaxy family names.

Info

Note that [each supported file type](/docs/filescan/3.1.1/metadefender-sandbox/2.2.0/datasheet/supported-file-types) has its own media type tag not listed here!

Analysis Tags (Sorted)Attention!

Color used for each tag does not represent the actual severity.

| Tag | Description |
| --- | --- |
| 64bits | Targets 64-bit architecture |
| adaptive-context | Threat indicator severity has been adjusted based on the adaptive context |
| adware | Displays unwanted ads or collects data for advertising purposes |
| aidetect | Web threat detection by AI models |
| anti-debug | Contains anti-debugging capabilities |
| anti-security | Attempts to disable or evade security tools |
| anti-vm | Detects virtual environments |
| apt | Found Advanced Persistent Threat-related activities |
| backdoor | Provides a backdoor for unauthorized remote access |
| banker | Targets financial data |
| base64 | Found Base64-encoded data or decoding functionality |
| bloated | Bloated executable to evade heuristic and malware analysis |
| botnet | Attempts botnet communication |
| byovd | Brings Your Own Vulnerable Driver to exploit kernel vulnerabilities |
| clickfix | Detection of ClickFix social engineering technique |
| compiled-script | Script compiled into an executable file |
| config-extracted | Malware configuration extracted |
| corrupted | Damaged or malformed file, often to evade analysis |
| cpl | Windows Control Panel |
| crypto | Involves cryptographic operations |
| delphi | Delphi programming language |
| disassembled | Contains disassembled code |
| dropper | Delivers additional payloads |
| embedequation | CExecutes code dynamically via NET reflectionontains embedded Office equation objects |
| evasive | Attempts to evade detection |
| exploit | Targets specific software vulnerabilities |
| expired-cert | Contains an expired certificate |
| fingerprint | Gathers system information to identify or profile the environment |
| geofencing | Enables malicious execution only in specific geographical regions |
| golang | Go programming language |
| greyware | Suspicious or potentially unwanted software (PUP) |
| hacktool | Detected hacktool artifacts |
| installer | Identified as known installer |
| invalid-signature | Contains a digital signature that is invalid or tampered with |
| keylogger | Contains keylogging capabilities |
| language-x | Identified language (being "x" the language code), which is often related to the attack target. Common codes are "uk" (Ukrainian), "ru" (Russian), or "zh" (Chinese) |
| large-file | A file unusually large, possibly bloated to hinder analysis |
| lolbin | Living-off-the-land binary |
| macros | Uses Office macros |
| macros-on-change | Executes code when the document is edited |
| macros-on-close | Executes code when the document is closed |
| macros-on-event | Executes code on specific user or system event |
| macros-on-open | Executes code when the document is open |
| masquerade | Pretends to be legitimate software to deceive users |
| metasploit | Linked to the Metasploit penetration testing framework |
| mirai | Detected Mirai artifacts |
| monikerlink | Exploits moniker-based links |
| msdt | Leverages Microsoft Support Diagnostic Tool for execution |
| next-stage-payload | Downloaded file from extracted malware config URL |
| obfuscated | Presents obfuscated data to evade detection |
| overlay | Contains an overlay, appended data at the end of the file |
| packed | Original executable has been packed to protect against analysis |
| persistence | Gains persistence to maintain presence after a reboot |
| phishing | Detected phishing attempt |
| ping | Uses ping tool for checking connectivity |
| polyglot | File which can be considered of multiple file types to bypass defenses |
| pyarmor | Obfuscates Python scripts with Pyarmor |
| pyinstaller | Python-compiled PE file with PyInstaller |
| qrcode | Uses QR codes |
| ransomware | Detected ransomware activities |
| rat | Detected Remote Access Trojan artifacts |
| reconnaissance | File capabilities include information discovery/enumeration about the target system |
| reflection | Executes code dynamically via NET reflection |
| remote-config | Malware configuration extracted from downloaded file |
| revoked-cert | Uses a certificate that has been revoked |
| self-signed-cert | Uses self-signed and untrusted certificate |
| sendkeys | Simulates user keystrokes |
| sfx | Self-extracting archive |
| shellcode | Contains malicious shellcode |
| signed | File is digitally signed |
| smb | Performs Server Message Block (SMB) communication |
| spyware | Monitors and exfiltrates sensitive user data |
| stealer | Targets sensitive data |
| stripped | Strips content to evade detection |
| tor | Attempts TOR communication |
| vbastomped | Detected VBA stomping to bypass detection |
| webdav | Exploits WebDAV protocol for file transfer |
| wix | Installer created using WiX toolset |
| zero-day | This threat has not been previously observed in OSINT databases and is not detected by any available antivirus engines |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
