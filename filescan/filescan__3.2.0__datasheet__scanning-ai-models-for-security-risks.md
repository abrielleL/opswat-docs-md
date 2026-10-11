<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/scanning-ai-models-for-security-risks -->

# Scanning AI Models for Security Risks

View as Markdown Ask ChatGPT about this page Ask Claude about this page

As AI becomes very popular in modern applications, companies are racing to integrate AI chatbots and other AI-powered utilities into their products to optimize work efficiency.

The sharing and reuse of pre-trained AI models has become a widespread practice. After training a model like ChatGPT, you need to save those weights (already trained model) somewhere. These files aren't just simple data - they're complex formats like Pickle, Pytorch and TensorFlow, each with their own serialization style.

Developers frequently download models from public repositories like Hugging Face, Kaggle, and others to accelerate innovation and avoid redundant training efforts. Attackers are now targeting the AI model supply chain by injecting malware, backdoors, and malicious logic into serialized model files. These compromised models can be difficult to detect using conventional security tools and may lead to remote code execution (RCE) attacks, data leak, or sabotage of downstream AI tasks.

MetaDefender Aether supports scanning AI model files, including `.pkl`, `.pt`, `.pb` and`.h5`, providing robust detection for the most critical attack vectors.

## [**Common AI Model Attack Vectors**](/docs/filescan/3.2.0/datasheet/scanning-ai-models-for-security-risks#common-ai-model-attack-vectors)

Several ML model formats can introduce security risks:

| Format | Framework | Extension | Description | Code Execution | Tagging |
| --- | --- | --- | --- | --- | --- |
| Pickle | Generic Python | `.pkl`, `.pickle` | Python’s default serialization format; allows arbitrary code execution during deserialization. | Yes | `pickle` |
| Pytorch | Pytorch | `.pt`, `pth` | Uses Pickle internally to store model weights and architecture, vulnerable to embedded code execution. | Yes | `pytorch` |
| Tensorflow | TensorFlow | `.pb` | Protocol Buffers format used to store SavedModels. Can include Lambda Layer in KerasMetadata to allow arbitrary code execution. | Yes | `tensorflow` |
| Keras | Keras / TensorFlow | `.h5` | HDF5 format used by Keras; Lambda layers serialized with marshal can enable code execution. | Yes | `tensorflow` |

## [**How MetaDefender Sandbox Enhances AI Model Security**](/docs/filescan/3.2.0/datasheet/scanning-ai-models-for-security-risks#how-metadefender-sandbox-enhances-ai-model-security)

MetaDefender Sandbox provides **comprehensive security analysis** for ML models, identifying potential threats before they can impact AI workflows.

### [**Key Capabilities**](/docs/filescan/3.2.0/datasheet/scanning-ai-models-for-security-risks#key-capabilities)

- **Support for Multi-Serialization Format Parsing:** Enables comprehensive detection across major AI model formats, including Pickle, Protocol Buffers, and Marshal serialization.
- **Leveraging Integrated Pickle Scanning Tools:** Integrates Fickling to parse Pickle’s structure and extract artifacts.
- **Deep Static Analysis:** Disassembles and analyzes serialized objects inside `pkl` , `pt` and `h5` files.
- **Graph-Level Threat Detection:** Identifies unsafe TensorFlow operators and custom graph nodes in `pb` models.
- **Uncovering Deliberate Evasion Techniques:** Exposes the hidden logic of complicated evasion techniques.

### [**Showcase Report: Detect Stack Pickle technique and its Malicious contents**](/docs/filescan/3.2.0/datasheet/scanning-ai-models-for-security-risks#showcase-report-detect-stack-pickle-technique-and-its-malicious-contents)

URL for the sample

<https://www.filescan.io/uploads/68bf95d2a1a41633174df884/reports/3bd2c3bf-8aa4-47bb-8b5b-fb4b5dbd0a90/overview>

Stacked Pickle can be utilized as a trick to hide malicious behavior. By nesting multiple Pickle objects and injecting the payload across layers then combined with compression or encoding. Each layer looks benign on its own, therefore many scanners and quick inspections miss the malicious payload.

MetaDefender Sandbox peels those layers one at a time: it parses each Pickle object, decodes or decompresses encoded segments, and follows the execution chain to reconstruct the full payload. By replaying the unpacking sequence in a controlled analysis flow, the sandbox exposes the hidden logic without running the code in a production environment.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
