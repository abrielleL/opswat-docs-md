<!-- source: https://www.opswat.com/docs/filescan/release-notes/release-notes-latest -->

# Release Notes for v3.3.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Date: 8th October 2026](/docs/filescan/release-notes/release-notes-latest#date-8th-october-2026)

Warning

**Direct upgrade not supported:** Versions earlier than 2.5.1 cannot be upgraded directly to v3.3.x.

**Recommended upgrade path:** Upgrade to 2.5.1 first, then install v3.3.X.

## [MetaDefender Aether™ v3.3.0 (including MetaDefender Sandbox™ capabilities)](/docs/filescan/release-notes/release-notes-latest#metadefender-aether-v330-including-metadefender-sandbox-capabilities)

With the release of MetaDefender Aether v3.3.0, Aether's analysis capability has now been extended to support LLM Scanning. This new capability will see Model Files both Statically and Dynamically analysed to ensure that they are clean from any threats.

Organizations are adopting open-source and third-party models faster than they can review them. An AI model is not just passive data. It can carry executable code and expose an interface that can be manipulated. A single model can compromise every system that loads it, or quietly act against the organization that deploys it.

The new [LLM Scanning](/docs/filescan/datasheet/scanning-ai-models-for-security-risks) feature makes Aether more powerful. It checks the model itself and how the model behaves:

- [LLM Static Analysis](/docs/filescan/datasheet/static-analysis) inspects the model file pre-execution, and finds hidden code that would run the moment the model is loaded.

- [LLM Dynamic Analysis](/docs/filescan/datasheet/dynamic-analysis) tests the running model with adversarial prompts. It shows whether the model can be hijacked or jailbroken, leaks data or produces harmful output.

Teams can now bring open-source and third-party models into their pipelines, registries and production systems with confidence.

## [Key features](/docs/filescan/release-notes/release-notes-latest#key-features)

### [**LLM Scanning**](/docs/filescan/release-notes/release-notes-latest#llm-scanning)

Submit a model to MetaDefender Aether in the same way you submit any other file. Aether runs two analyses: static analysis of the model file and dynamic analysis of the running model. If Aether finds a threat, Core blocks the file.

**Static analysis**

Aether never loads or runs the model. It reads only the parts of the file that can carry code or configuration and skips over the weights, so memory use stays low even for very large models.

| **Format** | **What Aether inspects** | **What it detects** |
| --- | --- | --- |
| Pickle and PyTorch | Every opcode, on a symbolic pickle VM | Code that runs on load, hidden imports, encoded and layered payloads built to evade simple scanners |
| SafeTensors | Header, tensor table and offsets | Malformed headers, out-of-bounds offsets, data hidden in bytes that no tensor covers |
| GGUF | Metadata, including the chat template | Jinja template injection |
| ONNX | Graph, nodes and external-data references | Path traversal, custom and Python-backed operators |
| Keras | Archive, model config and HDF5 attributes | Lambda-layer code execution, config-driven module loading |
| TensorFlow SavedModel | Graph and function library | Dangerous operators, such as Python execution |

Any payload Aether finds inside the file, including data hidden between tensors, is extracted and analysed on its own.

**Dynamic analysis**

Aether connects to your inference server through its OpenAI-compatible API and runs 38 attack probes against the live model with 600+ adversarial prompts, covering 9 of the OWASP Top 10 for LLM Applications categories.

| **OWASP category** | **Probes** | **What Aether tests** |
| --- | --- | --- |
| LLM01 Prompt Injection | 14 | Direct and indirect injection, agent data injection, jailbreaks and safety bypass, delayed instructions, encoding and Unicode tricks, roleplay framing, multi-step chaining |
| LLM02 Sensitive Information Disclosure | 6 | Leaks of sensitive data, credentials, personal data and documents; model extraction |
| LLM03 Supply Chain | 3 | AI supply chain compromise, hallucinated software packages, tool and context poisoning |
| LLM04 Data and Model Poisoning | 3 | RAG poisoning, persistent memory poisoning, training data poisoning |
| LLM05 Improper Output Handling | 5 | Unsafe code execution, insecure output, malware and exploit code, harmful content |
| LLM06 Excessive Agency | 1 | Misuse of agent tools |
| LLM07 System Prompt Leakage | 2 | System prompt leaks, guardrail and reasoning disclosure |
| LLM09 Misinformation | 3 | Disinformation, fraud and social engineering content, malicious automation |
| LLM10 Unbounded Consumption | 1 | Resource exhaustion and cost abuse |

**Examples include:**

- Prompt injection and jailbreaks, including encoded, multi-step and roleplay attacks
- Leaks of system prompts, credentials and personal data
- Requests for malware and exploit code
- Misuse of agent tools
- Resource exhaustion and cost abuse

Probes run in order of severity. Each scan plants single-use canary tokens, so if one appears in a response, the leak is confirmed. Every finding shows the prompt, the model's response, the severity, the OWASP category and the rule that flagged it.

Static and dynamic analysis are separate options, so you can run either one or both.

**MITRE ATLAS Mapping**

- Findings on AI models are now mapped to MITRE ATLAS, the MITRE framework for attacks on AI systems.
- ATLAS techniques are shown in the report, and you can filter reports by technique.
- The JSON report includes the ATLAS data, ready for your SIEM or SOAR.

### [**Searchable Threat Attribution**](/docs/filescan/release-notes/release-notes-latest#searchable-threat-attribution)

- **Advanced search:** Find every sample attributed to a malware family.
- **Packer attribution:** Native packers and .NET protectors are now identified separately.
- **Less noise:** Low-confidence attribution tags are no longer shown.
- **Extracted files:** Attribution found on an extracted file now also appears on the submitted file.

### [**More Evidence from Emulation**](/docs/filescan/release-notes/release-notes-latest#more-evidence-from-emulation)

- **HTTP traffic**: Emulation now records the full request and response for each HTTP call, including headers and body.
- **Delayed macros:** VBA emulation now supports Application.OnTime, which malware uses to delay its payload.

### [**Deeper Unpacking**](/docs/filescan/release-notes/release-notes-latest#deeper-unpacking)

- **Installers**: Better extraction from nested installers and more installer types, including PyInstaller, py2exe, ps2exe and Nuitka files.

## [**Improvements**](/docs/filescan/release-notes/release-notes-latest#improvements)

- **Usage Reporting:** Aether now shares anonymous usage metrics with OPSWAT through OpenTelemetry, to help us improve performance and prioritize the features you rely on. Only operational data is collected. No file contents, no personal data. Usage Reporting is on by default, and you can turn it off at any time in the Admin Panel.

## [**Awareness**](/docs/filescan/release-notes/release-notes-latest#awareness)

**Java 21 Notice for Adaptive Sandbox**

- This release includes a notification about an upcoming change to Adaptive Sandbox. A future Adaptive Sandbox feature will require Java 21, so customers should plan an upgrade from Java 17. Delivery of this feature is planned for the second half of 2027. No action is required at this time, and Adaptive Sandbox remains fully supported on Java 17. The notification is an early advisory to allow time for upgrade planning before the feature is released. Further details will be provided closer to the release date.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
