<!-- source: https://www.opswat.com/docs/filescan/datasheet/other-evasion---anti-analysis -->

# Other Evasion & Anti-Analysis

## [#1 Geofencing](/docs/filescan/datasheet/other-evasion---anti-analysis#1-geofencing)

**Detection Spotlight:** deep staticemulation

Malware documents employing geofencing have become a significant threat to cybersecurity. These malicious files often employ location-based triggers, making detection and mitigation a challenging task. However, Adaptive Threat Analysis stands out from traditional approaches by offering the capability to accurately emulate and falsify the expected geolocation values, effectively neutralizing the tactics employed by malware, thus enhancing our ability to protect against such threats.

In the sample provided below, we can observe a geofencing malware attempting to execute exclusively within a specific country. However, our innovative solution successfully bypasses this restriction, as previously mentioned, by emulating the desired geolocation values, demonstrating our superior capability in countering such geofencing-based threats.

URL for the sample

<https://www.filescan.io/uploads/643d529246e0911fda9eb28c/reports/65c685b3-a9ca-466d-9655-b6ab2ba0bf1a/emulation_data>

---

## [#2 Shellcode emulation](/docs/filescan/datasheet/other-evasion---anti-analysis#2-shellcode-emulation)

**Detection Spotlight:** deep staticemulation

Many application exploits bring their final payload in raw binary format (shellcode), which might be an obstacle when parsing the payload. With our shellcode emulation we are able to discover and analyse the behaviour of the final payload, in this example for a widely leveraged Office vulnerability in the equation editor. Hence opening the door to gathering the relevant IOCs.

URL to the sample

<https://www.filescan.io/uploads/650a09b733582f234efc873c/reports/f48778d5-8cde-4309-ad93-639e7a055e14/emulation_data>

---

## [#3 Highly obfuscated VBA macro](/docs/filescan/datasheet/other-evasion---anti-analysis#3-highly-obfuscated-vba-macro)

**Detection Spotlight:** deep staticemulation

Obfuscated VBA macros present a significant challenge to deliver a reasonable response time of active threats. This unclear code makes the analysis and understanding of threats a high complex task that demands a lot of time and effort. Our cutting-edge VBA emulation technology is able to overcome these challenges and provides a comprehensive analysis of obfuscated VBA macros together with clear insights into its functionality in seconds.

The analyzed sample is an Excel document with highly obfuscated VBA code that drops and runs a .NET DLL file, together with an LNK file in charge of continuing the malware execution chain. After VBA emulation, MetaDefender Aether identifies launched processes and the main deobfuscating function, automatically extracts obfuscated strings, and saves dropped files (previously hardcoded and encrypted in the VBA code). This rapidly shows the main purpose of the malware and gives us the possibility of further analysis of this threat.

URL to the sample

<https://www.filescan.io/uploads/6661fdc921581a92819b4d64/reports/e87e263e-27b5-45fc-bb99-733a553b3a36/overview>

Obfuscated VBA macro code

Extracted strings after deobfuscating and emulating the VBA macro code

Next stager PE file created by VBA emulation

---

## [#4 Sandbox evasion via Task Scheduler](/docs/filescan/datasheet/other-evasion---anti-analysis#4-sandbox-evasion-via-task-scheduler)

**Detection Spotlight:** emulation

Using Windows Task Scheduler to execute malicious payloads at a later time is a stealthy technique to evade sandbox environments seen in recent threats. It exploits the delay in execution to effectively bypass the short analysis window typical of sandboxes.

The following sample is an obfuscated VBScript that downloads the malicious payload and creates a scheduled task to run it 67 minutes later. Traditional sandboxes maintain the execution for only a few minutes and the malicious behavior would be never exposed. In the other hand, our VBScript emulator is able to detect and overcomes this evasion technique, adapting the execution environment to continue with further analysis, and getting the full report in 12 seconds.

URL to the sample

[Filescan.IO - Analysis Report for b161c8e32c0f33a182b5b2479521d3b826ce739ac0b3f3de9042e17d53873e57 - Emulation_data](https://www.filescan.io/uploads/66682a7d21581a92819c335a/reports/64374035-17a1-4c48-b810-f4fdf6f3f0d8/emulation_data)

Schedule task created to gain persistence and evade sandbox analysis (execution delayed 67 mins)

---

## [#5 .NET Reflection](/docs/filescan/datasheet/other-evasion---anti-analysis#5-net-reflection)

**Detection Spotlight:** emulation

NET Reflection is a powerful feature provided by the .NET framework that allows programs to inspect and manipulate a .NET file structure and behavior at runtime. It enables the examination of assemblies, modules, and types, as well as the ability to dynamically create instances of types, invoke methods, and access fields and properties.

Malware can use reflection to dynamically load and execute code from assemblies that are not referenced at compile time, allowing to fetch additional payloads from remote servers (or hidden in the current file) and execute them without writing them to disk, reducing the risk of detection.

In this case, we can see how the analysed VBScript loads and runs a .NET assembly into memory directly from bytes stored in a Windows register.

URL to the sample

<https://www.filescan.io/uploads/666b0289ef9fdf64aa6adb06/reports/ce3451fe-3dd6-40f2-bf06-44136f2fe43c>

VBScript saving a reversed and base64-encoded PE in a register and then running a .NET-based RAT using .NET reflection

Emulation actions showing the payload execution using .NET reflection

---

## [#6 Evasive Archive Concatenation](/docs/filescan/datasheet/other-evasion---anti-analysis#6-evasive-archive-concatenation)

**Detection Spotlight:** deep static

Attackers use archive concatenation to hide malware by appending multiple archives into a single file, exploiting how different tools process them. This technique creates multiple central directories - key structural elements used by archive managers - causing discrepancies during extraction and enabling the bypass of detection for malicious content hidden in overlooked parts of the archive.

MetaDefender Aether detects and extracts content from all concatenated archives, ensuring no file is missed and effectively neutralizing this evasive technique.

URL to the sample

<https://www.filescan.io/uploads/678f361f17177fed56b4bc54>

---

## [#7 Mitigating bloated executables](/docs/filescan/datasheet/other-evasion---anti-analysis#7-mitigating-bloated-executables)

**Detection Spotlight:** deep static

Threat actors bloat executables intentionally with junk data to evade detection by exploiting resource limitations and analysis time constraints in sandboxes. This evasion technique looks to overwhelm tools or bypass scans by exceeding time limits.

MetaDefender Aether detects bloated executables early, removes junk data, and processes a smaller file for efficient analysis. This debloating process targets various methods, including junk in overlays, PE sections, and certificates, ensuring accurate detection while conserving original resources.

URL to the sample

<https://www.filescan.io/uploads/67a5dcb5a55c685dbbf28985/reports/7be3e68b-7436-44c1-9eb5-fb041c800b2c/overview>

---

## [#8 Evasion through corrupted OOXML (office) documents](/docs/filescan/datasheet/other-evasion---anti-analysis#8-evasion-through-corrupted-ooxml-office-documents)

**Detection Spotlight:** deep static

Researchers discovered intentionally corrupted OOXML documents (modern office documents). By modifying the binary content near the internal file headers, the purposely broken files may be misdetected as ZIP files by automatic scans, which will attempt to extract compressed files.

Document viewers will automatically repair the document upon opening. At this point, despite the document containing phishing content, it may have effectively bypassed defenses. Automated analysis will not be able to read its content and therefore miss the relevant indicators.

URL to the sample

<https://www.filescan.io/uploads/676172737e0ef1ddadddf145/reports/10075c64-30f4-4215-9eef-e41078dcb205/overview>

---

## [#9 Document targeting critical infrastructures](/docs/filescan/datasheet/other-evasion---anti-analysis#9-document-targeting-critical-infrastructures)

**Detection Spotlight:** deep staticemulation

This Office document targets critical infrastructure in Iran (with content in Persian) to steal sensitive information, such as credentials and documents, and periodically takes screenshots, potentially for espionage purposes.

After establishing persistence, it performs a stealthy initial internet connectivity check (against a trusted domain like google.com) to ensure a reliable connection, delaying further actions until network conditions allow the attack to proceed. This is a tactic commonly observed in attacks on critical infrastructure, environments where internet access may be intermittent or restricted.

URL to the sample

<https://www.filescan.io/uploads/679664ec0a04287e8b028aff/reports/894ab8c8-f6e4-4030-8414-ea2715ad64f9/emulation_data>

---

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
