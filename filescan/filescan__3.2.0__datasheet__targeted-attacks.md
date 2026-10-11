<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/targeted-attacks -->

# Targeted Attacks

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [#1 APT spear-phishing targeting government sectors in the Middle East](/docs/filescan/3.2.0/datasheet/targeted-attacks#1-apt-spear-phishing-targeting-government-sectors-in-the-middle-east)

**Target Profile:** diplomatic maritime military governementmiddle east

**Threat Actor:** APT34 Oilrig Karkoff

**Detection Spotlight:** emulationfile extraction

The origin of the files is reportedly part of a spearphishing email, either attached to the email or downloaded from a link included in the email. After some research, we discovered that the sample was first spotted in 2021 and associated with APT34. The original filename is “جهوزية الزوارق والمراكب.doc”, which translates to English as “Boat and vessel readiness.doc”. The lure content of the document aligns with its title, using Lebanese Navy information that was reportedly potentially stolen during a previously reported compromise. The document prompts to enable macros. If enabled, it creates a directory pretending to be related to Google in order to remain unnoticed, where it drops 3 files. It also creates a scheduled task to execute one of three files: a small VBA script which uses Powershell to load the other two files through .NET Assembly reflection. These two other files that are detected and extracted in the analysis are .NET DLLs, samples of the Karkoff malware family.

Aether researchers were able to hunt this sample by searching for themed documents filtering by specific languages, allowing them to spot interesting samples such as this, implemented to target government sectors in the Middle East.

Info

[h](https://www.filescan.io/uploads/696fa5805db9ae47708a66dd)[ttps://www.filescan.io/uploads/6913e57a935d9f0d73ceb189/reports/a34defcd-dc41-491f-ab33-6954acc86efe/overview](https://www.filescan.io/uploads/6913e57a935d9f0d73ceb189/reports/a34defcd-dc41-491f-ab33-6954acc86efe/overview)

---

---

## [#2 APT spear-phishing campaign using in-house protected macros](/docs/filescan/3.2.0/datasheet/targeted-attacks#2-apt-spear-phishing-campaign-using-in-house-protected-macros)

**Target Profile:** pakistan south asia manufacturing

**Threat: APT-C-35** donot

**Detection Spotlight:** emulation

This campaign is attributed to a South Asia–focused APT conducting highly targeted intrusions against organizations with business, industrial, or government relevance. The actor relies on spear-phishing emails for initial access, showing clear signs of victim profiling rather than mass distribution.

Malware is delivered via a malicious Office document, with the correct macro password included in the email body. The macro uses an in-house password check, meaning the malicious logic will not execute unless the correct password is entered, a mechanism that is especially effective at preventing automated analysis systems. It also includes a meaningless loop to waste analysis resources, dynamically generates shellcode, and executes it by abusing the callback mechanism of the Windows *CryptEnumOIDInfo* API, helping the payload evade detection.

Info

<https://www.filescan.io/uploads/6970eca85db9ae47708bfcdb/reports/39bb8f35-499e-4353-a0f1-0e8ec4504956/overview>

---

#3 Stealthy connectivity check before data exfiltration

**Target Profile:** iran cyberespionage

**Threat Actor: stealer**

**Detection Spotlight:** deep static emulation

This Office document targets critical infrastructure in Iran (with content in Persian) to steal sensitive information, such as credentials and documents, and periodically takes screenshots, potentially for espionage purposes.

After establishing persistence, it performs a stealthy initial internet connectivity check (against a trusted domain like google.com) to ensure a reliable connection, delaying further actions until network conditions allow the attack to proceed. This is a tactic commonly observed in attacks on critical infrastructure, environments where internet access may be intermittent or restricted.

Info

<https://www.filescan.io/uploads/679664ec0a04287e8b028aff/reports/894ab8c8-f6e4-4030-8414-ea2715ad64f9/emulationdata>

---

---

## [#4 MuddyWater “Cybersecurity Guidelines” maldoc](/docs/filescan/3.2.0/datasheet/targeted-attacks#4-muddywater-cybersecurity-guidelines-maldoc)

**Target Profile:** middle east diplomatic maritime financial telecom

**Threat: MuddyWater**

**Detection Spotlight:** emulation

A spearphishing email titled “Cybersecurity Guidelines”, sent from a legitimate account tied to a regional mobile operator, delivers a malicious Word document. Once the victim enables macros, the VBA code extracts a hex-encoded payload embedded inside the document (stored in a UserForm control), cleans it up, decodes it back into a Windows executable, writes it to disk, and launches it immediately. The launch step is handled through an obfuscated wrapper that rebuilds key strings at runtime to make the macro logic harder to follow.

That dropped executable is a Rust-based implant (“RustyWater”) that adds multiple defensive layers. It sets up anti-debug/anti-tamper behavior (e.g., registering a Vectored Exception Handler), keeps operational strings encrypted (position-independent XOR), and performs basic security-product discovery by checking for AV/EDR artifacts (agent files, service names, install paths) across 25+ tools. It also establishes persistence via a Run-key autostart entry, and uses HTTP-based C2 with layered obfuscation (JSON → Base64 → XOR) plus randomized callback timing (jitter). The execution can be further masked via injection into a legitimate Windows process.

Researchers found evidence of additional activity targeting the UAE, including decoy documents and impersonation-themed lures, suggesting a broader regional targeting set.

Info

<https://www.filescan.io/uploads/6961a589d1d688e1d664a396/reports/84de06f5-5229-457c-9a07-af2c81ec7f8e/overview>

---

---

## [#5 Threat actor delivers targeted multistage polyglot malware](/docs/filescan/3.2.0/datasheet/targeted-attacks#5-threat-actor-delivers-targeted-multistage-polyglot-malware)

**Target Profile:** aviation telecom transportation

**Threat: UNK_CraftyCamel**

**Detection Spotlight: deep static** emulation

This campaign is a highly targeted espionage operation against a very small number of organizations in the UAE, mainly in the aviation, satellite, and transportation sectors. The emails are carefully crafted and sent from a compromised legitimate Indian company, which helps build trust. While there is no confirmed APT attribution, the targeting and techniques overlap with Iran-aligned threat activity, suggesting a likely state-linked actor.

The attack is notable for its extensive use of polyglot files, which are valid in multiple formats at once. Victims receive a ZIP containing a fake Excel file that is actually a LNK shortcut, along with PDF/HTA and PDF/ZIP polyglots. These files abuse trusted Windows tools like mshta.exe to run hidden code, evade detection, and load the final payload disguised as an image.

Info

<https://www.filescan.io/uploads/696fa5805db9ae47708a66dd>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
