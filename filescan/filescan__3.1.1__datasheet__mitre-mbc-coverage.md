<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/mitre-mbc-coverage -->

# MITRE MBC Coverage

### [**MITRE ATT&CK Coverage in Our MetaDefender Aether Solution**](/docs/filescan/3.1.1/datasheet/mitre-mbc-coverage#mitre-attck-coverage-in-our-metadefender-aether-solution)

While our sandbox already maps malicious behaviors to the MITRE ATT&CK framework, we decided to incorporate MITRE MBC (Malware Behavior Catalog) to complement ATT&CK and enhance the depth of our behavioral analysis. ATT&CK excels at describing adversary tactics and techniques at an operational level, particularly around how threats interact with systems and users. However, some low-level malware behaviors fall outside ATT&CK’s intended scope.

MITRE MBC focuses exactly on those intrinsic characteristics that define how malware families operate. These behaviors are key to understanding evasion patterns, classifying variants, and identifying emerging trends in malware development. By combining ATT&CK and MBC, our sandbox provides a more complete analytical view:

- ATT&CK captures high-level intent and adversary techniques.
- MBC captures the technical behaviors and building blocks inside the malware itself.

The result is stronger and more actionable reporting for detection engineering, malware research, and threat intelligence teams. Rather than replacing ATT&CK, MBC reinforces it by filling natural gaps while maintaining full alignment with industry-standard frameworks.

Aether's behavioral detection engine provides broad coverage across the MITRE Malware Behavior Catalogue, with particularly strong depth in the Anti-Behavioral Analysis category. Aether accurately identifies malware that actively attempts to evade analysis environments, detecting behaviors related to debugger detection and evasion, sandbox awareness, virtual machine detection, and dynamic analysis evasion techniques.

Beyond anti-analysis behaviors, Aether covers a wide range of Defense Evasion, Discovery, and Communication tactics. This includes the detection of software packing and obfuscation, process injection, execution flow hijacking, and covert data storage techniques. On the discovery side, Aether identifies attempts to enumerate the host environment and detect analysis tooling. It also tracks network-level behaviors such as DNS, FTP, and ICMP communication patterns, as well as granular operating system interactions like registry manipulation, giving analysts a comprehensive view of what a sample is doing across the full attack lifecycle.

MITRE MBC Coverage

You can check the MBC matrix by clicking in [here](https://uploads.developerhub.io/prod/XX2D/v7c6kbi6vknqcjw6zdzvh33ssv69ypkl7req9xlwnl0lw40fryzbvkn9xcusdg4j.svg).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
