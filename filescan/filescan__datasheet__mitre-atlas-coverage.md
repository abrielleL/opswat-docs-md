<!-- source: https://www.opswat.com/docs/filescan/datasheet/mitre-atlas-coverage -->

# MITRE ATLAS Coverage

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [MITRE ATLAS Coverage in Our MetaDefender Aether Solution](/docs/filescan/datasheet/mitre-atlas-coverage#mitre-atlas-coverage-in-our-metadefender-aether-solution)

MITRE ATLAS (Adversarial Threat Landscape for AI Systems) catalogues how adversaries reconnoiter, compromise, and abuse AI systems, organized across 16 tactics. In MetaDefender Aether, we map our AI threat detection to ATLAS so that our detection capabilities are expressed in the same vocabulary the community widely uses to describe AI threats.

Our detection capabilities focus on key tactics within the framework, such as:

- **Resource Development & Initial Access** (e.g., publish poisoned AI artifacts, AI supply chain compromise)
- **Execution & Persistence** (e.g., prompt injection, unsafe artifact deserialization, backdoored model weights)
- **Privilege Escalation & Defense Evasion** (e.g., jailbreak, prompt obfuscation, format masquerading, corrupted model files)
- **Discovery & Exfiltration** (e.g., system prompt extraction, model information discovery, training data leakage)

We provide broad coverage across the MITRE ATLAS matrix, spanning **13 of the 16 tactics** and 44% of catalogued techniques, with particularly strong depth in the Defense Evasion category. We accurately identify adversarial prompting that attempts to bypass model safeguards, detecting behaviors related to jailbreak, prompt obfuscation, and trusted output component manipulation. Coverage extends to artifact-level threat vectors as well, including unsafe deserialization, corrupted model files, and obfuscated payloads embedded in model file structures.

### [MITRE ATLAS Matrix](/docs/filescan/datasheet/mitre-atlas-coverage#mitre-atlas-matrix)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
