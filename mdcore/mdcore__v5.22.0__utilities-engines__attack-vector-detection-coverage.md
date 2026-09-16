<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage -->

# Attack Vector Detection Coverage

## [Overview](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#overview)

The MetaDefender Core YARA engine provides comprehensive threat detection across the attack lifecycle, from initial delivery through execution and evasion. This analysis examines 80+ hand-picked and high efficiency detection rules across 10 major attack vector categories, focusing on the threats our engine identifies and the detection strategies employed.

### [Attack Vectors Covered:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#attack-vectors-covered)

1. **Document-Based Attack Vectors** - Malicious Office documents, PDFs, and RTF files
2. **Script and Macro-Based Execution** - PowerShell, JavaScript, VBA, and scriptlet attacks
3. **Encoding and Obfuscation Techniques** - Base64, XOR, hex encoding, and multi-layer obfuscation
4. **PE Structure Manipulation and Evasion** - Executable format modifications and packing
5. **Import Table and Dynamic Loading** - API hiding and dynamic resolution techniques
6. **Embedded Content and Payload Hiding** - Hidden executables in resources and overlays
7. **Network and Communication Vectors** - C2 channels and legitimate service abuse
8. **Shortcut and Link Abuse** - Malicious LNK files and hyperlink manipulation
9. **Cryptographic and Encoding Functions** - Encryption libraries and protocol obfuscation
10. **Anti-Analysis and Evasion** - VM detection and environment fingerprinting

---

## [1. Document-Based Attack Vectors](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#1-document-based-attack-vectors)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Document-based attacks exploit legitimate file formats to deliver payloads or execute malicious code, leveraging user trust in common document types.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Key rules in this category include such as `FC_Encrypted_Office_Document` which identifies encrypted documents used to bypass security scanning, and `FC_PDF_Launch_Function` which catches PDFs with dangerous execution capabilities. `FC_Office_Document_with_VBA_Project` detects macro-enabled documents, among other document-based detection rules.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Microsoft Office Documents
- PDF
- OLE (Object Linking and Embedding)
- Email Attachments
- OneNote
- Exploits

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1204.002 - Malicious File (User Execution)**](https://attack.mitre.org/techniques/T1204/002/)
- [**T1137 - Office Application Startup**](https://attack.mitre.org/techniques/T1137/)
- [**T1566.001 - Spearphishing Attachment**](https://attack.mitre.org/techniques/T1566/001/)

---

## [2. Script and Macro-Based Execution](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#2-script-and-macro-based-execution)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Script-based attacks leverage legitimate system interpreters to execute malicious code, using "living off the land" techniques with PowerShell, JavaScript, VBA and such script languages.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Notable examples include `FC_File_with_JavaScript_Script_Block` which detects JavaScript script blocks in files, and `FC_Scripting_VB` which identifies Visual Basic scripting content. `SC_JavaScript_Double_Indirect_Call` targets sophisticated JavaScript indirection methods, representing several of the script execution detection capabilities.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- JavaScript in HTML
- Script Execution
- Microsoft Shortcut (LNK)
- Exploits

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1059.001 - PowerShell**](https://attack.mitre.org/techniques/T1059/001/)
- [**T1059.005 - Visual Basic**](https://attack.mitre.org/techniques/T1059/005/)
- [**T1059.007 - JavaScript/JScript**](https://attack.mitre.org/techniques/T1059/007/)

---

## [3. Encoding and Obfuscation Techniques](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#3-encoding-and-obfuscation-techniques)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Obfuscation and encoding techniques hide malicious content from static analysis and security tools using various encoding schemes and data manipulation methods.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Among the obfuscation detection rules, `pe_double_base64d_pe` identifies executables encoded twice with Base64 for sophisticated evasion, and `pe_resource_single_byte_xor_PE` detects XOR-based obfuscation in PE resources. `FC_File_with_UTF8_and_Base64_Encoded_Strings` identifies multi-layer encoding schemes across different file formats, illustrating the breadth of encoding detection methods.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Encoding
- Resources, overlay, and embedded files

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1027 - Obfuscated Files or Information**](https://attack.mitre.org/techniques/T1027/)
- [**T1140 - Deobfuscate/Decode Files or Information**](https://attack.mitre.org/techniques/T1140/)

---

## [4. PE Structure Manipulation and Evasion](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#4-pe-structure-manipulation-and-evasion)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

PE structure manipulation involves modifying executable file structures to evade analysis tools while maintaining functionality, using techniques like header anomalies and section manipulation.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Representative rules include `pe_section_rwx` which identifies dangerous read-write-execute sections used for dynamic code generation, and `pe_high_entropy_section` using entropy analysis to detect packed or encrypted content. `pe_overlapping_sections` catches deliberate PE manipulation designed to confuse analysis tools, showcasing the engine's comprehensive PE analysis capabilities.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- PE Header
- PE Sections
- PE Imports
- Signature

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1027.002 - Software Packing**](https://attack.mitre.org/techniques/T1027/002/)

---

## [5. Import Table and Dynamic Loading](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#5-import-table-and-dynamic-loading)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Import table manipulation hides malware functionality by using dynamic API resolution instead of static imports, making analysis more difficult.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Standout detection methods include `pe_dynamic_api_resolution_imports` which identifies the classic LoadLibrary/GetProcAddress pattern used to hide functionality, and `pe_zero_imports` which catches completely import-free executables (often indicating packing). `pe_imports_by_ordinal` targets obfuscated imports using ordinal numbers instead of function names, demonstrating various approaches to import analysis.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- PE Imports

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1055 - Process Injection**](https://attack.mitre.org/techniques/T1055/)
- [**T1129 - Shared Modules (Dynamic Loading)**](https://attack.mitre.org/techniques/T1129/)
- [**T1027.002 - Software Packing**](https://attack.mitre.org/techniques/T1027/002/)

---

## [6. Embedded Content and Payload Hiding](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#6-embedded-content-and-payload-hiding)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Payload hiding techniques leverage file structures to conceal malicious content within legitimate containers, using resources, overlays, and encoding methods.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Prominent examples include `pe_embedded_pe` which identifies executables hiding other PE files using header-independent detection, and `pe_resource_base64d_pe` which catches Base64-encoded executables concealed in resource sections. `pe_large_overlay` flags suspiciously oversized overlays used for payload storage, reflecting the diverse payload hiding detection techniques available.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Resources, overlay, and embedded files

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1105 - Ingress Tool Transfer**](https://attack.mitre.org/techniques/T1105/)
- [**T1027 - Obfuscated Files or Information**](https://attack.mitre.org/techniques/T1027/)

---

## [7. Network and Communication Vectors](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#7-network-and-communication-vectors)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Network-based vectors encompass delivery mechanisms and communication channels, often abusing legitimate services to blend with normal traffic.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Selected examples include `FC_File_with_Amazon_SES_Redirect` which identifies abuse of legitimate Amazon email services for malware distribution, and `FC_WinHttpRequest_Object` which detects embedded HTTP objects used for C2 communication. `FC_FTP_Credentials` catches embedded authentication data suggesting exfiltration preparation, highlighting key network-based threat detection capabilities.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Application Layer Protocols
- URL Redirection and External Services

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1041 - Exfiltration Over C2 Channel**](https://attack.mitre.org/techniques/T1041/)
- [**T1567 - Exfiltration Over Web Service**](https://attack.mitre.org/techniques/T1567/)
- [**T1071 - Application Layer Protocol**](https://attack.mitre.org/techniques/T1071/)

---

## [8. Shortcut and Link Abuse](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#8-shortcut-and-link-abuse)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Shortcut and link abuse leverages LNK files and hyperlinks to execute commands or redirect users while appearing as harmless shortcuts.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

The primary rules in this limited category are `SC_Microsoft_LNK_Commands` which identifies malicious shortcuts with complex command sequences used for script execution or payload downloading, and `FC_HTML_JavaScript_with_Hyperlink_Reference` which detects JavaScript-based hyperlink manipulation. These rules target user execution tricks and social engineering tactics that exploit trust in familiar link formats.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Microsoft Shortcut (LNK)

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1547.009 - Shortcut Modification**](https://attack.mitre.org/techniques/T1547/009/)
- [**T1204.002 - Malicious File (User Execution)**](https://attack.mitre.org/techniques/T1204/002/)

---

## [9. Cryptographic and Encoding Functions](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#9-cryptographic-and-encoding-functions)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Cryptographic and encoding functions detect the presence of encryption libraries and encoding schemes used for payload protection or communication encryption.

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Core examples from this category include `FC_File_with_CryptoJS_Decrypt_Function` which identifies suspicious CryptoJS usage in documents where it's unexpected and often malicious, and `FC_File_with_CryptoJS_Encode_Function` which detects CryptoJS encoding functions. These rules address cryptographic library usage in unexpected contexts, among other cryptographic detection methods.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Encoding

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1573 - Encrypted Channel**](https://attack.mitre.org/techniques/T1573/)
- [**T1027 - Obfuscated Files or Information**](https://attack.mitre.org/techniques/T1027/)

---

## [10. Anti-Analysis, Evasion and Privilege Elevation](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#10-anti-analysis-evasion-and-privilege-elevation)

### [Description](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#description)

Anti-analysis techniques detect and evade security analysis environments, ensuring malware only executes in intended target systems. Such attacks include

### [Detection Examples:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#detection-examples)

Notable examples include `SC_User_Access_Control_Bypass` which identifies techniques to bypass Windows User Access Control for privilege escalation, and `pe_unusual_entrypoint_section` which detects executables with entry points in unexpected sections used to evade analysis. These complement our more sophisticated anti-analysis detection capabilities deployed across the engine.

### [Required Rule Groups:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#required-rule-groups)

- Archive files and packing techniques
- Exploits
- PE Header

### [Key Associated MITRE ATT&CK Techniques:](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#key-associated-mitre-attck-techniques)

- [**T1497 - Virtualization/Sandbox Evasion**](https://attack.mitre.org/techniques/T1497/)

---

## [Rule Group Mapping Note](/docs/mdcore/v5.22.0/utilities-engines/attack-vector-detection-coverage#rule-group-mapping-note)

The rule group categorizations provided in the "Required Rule Groups" sections represent a best-effort mapping between the existing rule group structure and the attack vector categories. While these mappings provide comprehensive coverage for each attack vector, they are not perfect 1:1 matches due to the different organizational approaches between rule groups and attack vector classifications. Some rule groups may contain rules that extend beyond the specific attack vector category, and some attack vectors may benefit from rules in multiple groups. The suggested groupings are designed to provide optimal detection coverage for each attack vector category.
