<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/metadefender-aether-for-coreo9z -->

# MetaDefender Aether for Core

**MetaDefender Aether for Core** is an advanced threat detection and analysis module for the MetaDefender Core platform. It provides a powerful layer of security by integrating a dynamic, emulation-based adaptive sandbox that performs behavioral analysis on files to detect and prevent zero-day threats and sophisticated evasive malware.

Designed for seamless integration, particularly in air-gapped and regulated environments, Aether for Core enhances MetaDefender Core's static analysis capabilities with real-time dynamic threat intelligence.

**1. Core Features and Capabilities**

- **Adaptive Threat Analysis**: At its core, the module uses a dynamic sandbox to detonate files in a controlled, emulated environment. This allows for the observation of file behavior to identify malicious actions, such as ransomware encryption, malicious process injection, or command-and-control (C2) communication. This complements MetaDefender Core’s multi-engine scanning and Deep CDR (Content Disarm and Reconstruction) technologies.
- **Advanced Zero-Day Threat Detection**: By focusing on behavioral patterns rather than signatures, Aether for Core is highly effective against unknown, polymorphic, and obfuscated malware that bypasses traditional antivirus engines. It identifies Indicators of Compromise (IOCs) in real-time and correlates threat patterns to known malware families and campaigns.
- **Integrated Threat Intelligence**: The module includes an additional reputation engine that provides real-time checks for URLs, IPs, and domains associated with malware, phishing, and botnets. This service is available for both online and offline deployments, providing a critical layer of defense against known malicious infrastructures.
- **Threat Scoring and Prioritization**: All detected threats are assigned a risk level and a threat score. This allows security teams to prioritize remediation efforts and quickly respond to the most critical threats through the MetaDefender Core dashboard.

**2. Integration and Workflow**

- **Seamless Integration**: Aether for Core is an embedded module within MetaDefender Core. Activation is achieved by simply adding the appropriate API key. All configuration, policy management, and reporting are handled within the MetaDefender Core management interface.
- **Policy-Driven Workflow**: Administrators can create custom policies to define which files should be sent to the sandbox for analysis. This can be based on file type, risk level determined by heuristic analysis, or triggers from Deep CDR (e.g., the presence of macros in a document). This policy-driven approach minimizes performance overhead by ensuring that only the highest-risk files undergo dynamic analysis.
- **Unified Reporting**: Sandbox analysis results, including detailed verdicts, threat scores, and extracted IOCs, are displayed directly within the MetaDefender Core UI. This provides a single pane of glass for all threat data, from multi-engine AV scans to Deep CDR and dynamic analysis.

**3. Deployment**

MetaDefender Aether for Core supports a variety of deployment options to meet diverse infrastructure and regulatory requirements, including:

- On-premises
- Cloud (AWS, Azure, GCP)
- Containerized environments (Docker, Kubernetes)

**4. Use Cases**

- **Securing Data in Transit**: Enhancing the security of file uploads, email attachments, and data transfers through ICAP-enabled devices or MFTs (Managed File Transfers).
- **Critical Infrastructure Protection**: Providing advanced threat detection for air-gapped and highly regulated environments where cloud-based analysis is not an option.
- **Security Operations (SOC) Enablement**: Equipping security analysts with detailed behavioral analysis and forensic data to aid in incident response and threat hunting.

**5. Summary**

MetaDefender Aether for Core is a critical component for organizations seeking to build a comprehensive defense against advanced cyber threats. By combining the static analysis capabilities of MetaDefender Core with the dynamic, behavioral analysis of a sandbox, it offers a multi-layered security approach that is both highly effective and seamlessly integrated. Its flexible deployment options and policy-driven workflow make it an ideal solution for any organization looking to enhance its zero-day threat detection capabilities without adding significant operational complexity.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
