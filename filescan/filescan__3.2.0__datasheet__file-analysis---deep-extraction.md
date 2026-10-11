<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction -->

# File Analysis & Deep Extraction

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [#1 Synthetic (fabricated) sample](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#1-synthetic-fabricated-sample)

**Detection Spotlight:** deep staticunpackingemulationmalware config

This sample stands as a purpose-built example to highlight the diverse capabilities of **MetaDefender Sandbox** (previously known as OPSWAT Filescan Sandbox). Crafted to show-off real-world cyber threats, embedding multiple files and file-types into each other. This effectively demonstrates our solution's prowess in adaptive threat analysis, behavioral analysis, and advanced security measures.

Check out all the following great features of the previous link:

- Many detailed indicators, highlighting these:

  - Significant evidence of malicious (phishing) file
  - Malware config
  - Many PE related ones
  - Call for action indicators
  - Contains an URL encoded in a QR code

    - We do decode QR codes even if they're embedded. Check this out both as an indicator, as strings and as the picture itself rendered
- File details shown in additional files, make sure you are not only checking the input, but all the details of:

  - Extracted files (different file types with many details shown!)
  - Downloaded files
- Emulation data - note that we're able to dig down multiple levels into the emulation. Check some of the interesting blocks, such as:

  - AccessLocale
  - StartProcess
  - CreateObject
- Identified sets of IOCs, including the URL from the QR code as well
- Thorough string extraction with the filtering ability

URL for the sample

<https://www.filescan.io/uploads/6551fb8d2546bd423f181cc3/reports/cc034b35-24c0-4b01-a75d-84a9c7639c59/overview>

---

## [#2 Threat Pattern Correlator](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#2-threat-pattern-correlator)

**Detection Spotlight:** simsearchAI detection

Employing Threat Pattern Correlator functionality, sandbox has detected a file remarkably resembling a known malware. Notably, this file had been previously marked as non-malicious, revealing the potential for false negatives in our security assessments. This discovery empowers us to specifically target and rectify these overlooked threats.

It is important to highlight that Threat Pattern Correlato is highly valuable for threat research and hunting, as it can help uncover samples from the same malware family or campaign, providing additional IOCs or relevant information about specific threat activities.

[Learn more about this feature by clicking here.](/docs/filescan/3.2.0/datasheet/threat-pattern-correlator)

URL for the sample

<https://www.filescan.io/uploads/682b67e1c609634bd7c989af/reports/53383651-1d20-490a-82fb-c5f476599f71/similarity_search>

---

## [#3 Finding interesting things via Disassembly](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#3-finding-interesting-things-via-disassembly)

### [#3.1 Native executable](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#31-native-executable)

**Detection Spotlight:** deep static

Our disassembling engine revealed intriguing findings within the target sample. Surprisingly, this sample monitors the system time using the uncommon `rdtsc` instruction and accesses an internal, undocumented structure in Windows, commonly used for different malicious tricks. These unusual actions raise questions about its purpose and underscore the need for further investigation to assess potential risks to the system.

URL for the sample

<https://www.filescan.io/uploads/6437de44b4ec50bace5ff564/reports/a74af3b9-596f-4de8-8a82-f63e025e75d5/disassembly>

### [#3.2 .NET Executable](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#32-net-executable)

**Detection Spotlight:** deep static

The sample under examination was built using .NET framework. While we refrain from displaying the actual CIL, our decompilation process extracts and presents noteworthy information, including strings, registry artifacts, and API calls.

Besides that, we parse the .NET metadata to identify .NET-specific functions and resources. This process allows to extract detailed information about the assembly, such as methods, classes, and embedded resources, which is critical for analyzing the behavior and structure of .NET applications.

URL to the sample

<https://www.filescan.io/uploads/671257087f0507a8d241e285/reports/c80b84e5-5431-4ebc-9c35-56cc7921ec71/overview>

---

## [#4 Malware config extraction of a packed sample](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#4-malware-config-extraction-of-a-packed-sample)

**Detection Spotlight:** unpackingmalware config

The sample below reveals a malware that was packed using the UPX packing technique. Despite its attempt to evade detection and defenses, our analysis successfully unpacked the payload, exposing its true identity as a Dridex Trojan. We were able to uncover the malware configuration, shedding light on the malicious intent behind this threat, extracting valuable IOCs.

[Learn more about malware config extraction feature by clicking here.](/docs/filescan/3.2.0/datasheet/supported-malwares-for-config-extraction)

[Learn more about malware unpacking feature by clicking here.](/docs/filescan/3.2.0/datasheet/supported-packers-for-unpacking)

URL for the sample

<https://www.filescan.io/uploads/6710df185c4ea75bc80ab7e0/reports/9e0ef23b-fbc1-4a56-af25-01dc3d3671c3/overview>

---

## [#5 XOR decrypting payload stored in PE resource](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#5-xor-decrypting-payload-stored-in-pe-resource)

**Detection Spotlight:** deep staticunpacking

This feature enables to reveal hidden artifacts encrypted within PE resources. Malicious artifacts are often encrypted to evade detection and obscure the true intent of the sample. Uncovering these artifacts is essential, as they typically contain critical data (as C2 information) or payloads. By extracting them, the sandbox can deliver a deeper scan, with higher chance of identifying the most valuable IOCs.

Both storing encrypted data in a PE resource and using XOR encryption are techniques widely used by malware for these two basic reasons:

- Storing payloads in PE resources helps malware evade detection by static analysis tools. Many security tools focus on analyzing the executable’s main code section, while resources are often overlooked, making it easier to hide malicious content.
- XOR encryption shines for its simplicity and efficiency in evading detection, being time and resource efficient.

But XOR encryption has a weakness when applied to data with a large number of null bytes (such as PE files). This is because if a bit is XORed with 0, the original bit remains unchanged. By analyzing patterns in the encrypted data, especially in areas with many null bytes, the encryption key can be revealed, allowing to decrypt the hidden.

URL to the sample

<https://www.filescan.io/uploads/66ab4c2e78d5c73fb1ca7f90/reports/eec0ead1-4ba2-4d6d-acf3-8ca73f9bec6f/overview>

---

## [#6 Stealthy .NET Loader with Bitmap Payload](/docs/filescan/3.2.0/datasheet/file-analysis---deep-extraction#6-stealthy-net-loader-with-bitmap-payload)

**Detection Spotlight:** deep staticunpackingmalware config

RoboSki is the most commonly observed .NET loader in recent years. This loader hides a multi-stage payload chain behind legitimate code and image resources. It decrypts a bitmap image to load a fileless .NET DLL, protected with ConfuserEx, which finally drops the final payload.

This threat uses obfuscation, runtime decryption, and fileless techniques to evade static detection. Threat insights are protected, making crucial actionable intelligence not accessible by simple detonating the sample — and manual unpacking is time-consuming and error-prone.

Why removing protection layers matters? Mitigating protection layers (like ConfuserEx control-flow obfuscation and string encryption) is crucial because it restores readable logic, making code actionable for detection and analysis.

Sandbox Highlights

- Unpacks .NET loaders automatically — including protected stages.
- Removes control-flow obfuscation to expose real logic and increase unpacking successful rate.
- Extracts hidden payloads and configs (C2s, persistence, stealing hooks) in one pass.

Attack Timeline VS Sandbox Analysis

URL for the sample

<https://www.filescan.io/uploads/686faccc80b46be06e9dbbdf/reports/21f43b71-56bf-4494-a2d2-9b76ff75d17c>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
