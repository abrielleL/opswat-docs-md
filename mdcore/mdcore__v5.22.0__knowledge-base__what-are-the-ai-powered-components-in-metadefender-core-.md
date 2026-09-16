<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-are-the-ai-powered-components-in-metadefender-core- -->

# What are the AI-Powered Components in MetaDefender Core?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

MetaDefender Core includes several components that leverage artificial intelligence (AI) and machine learning technologies to enhance detection accuracy, contextual understanding, and adaptive threat analysis. This article describes which components have AI-powered features and how they contribute to overall threat prevention.

### [1. **Metascan (Anti-Malware Engines)**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-ai-powered-components-in-metadefender-core-#1-metascan-anti-malware-engines)

Depending on the antivirus (AV) engines licensed and enabled in your environment, MetaDefender Core can utilize AI-driven detection models provided by certain vendors. These models are used to detect previously unseen or polymorphic malware based on behavior or heuristic patterns rather than static signatures.

For details on which AV engines include AI capabilities, refer to the official documentation below: [MetaDefender Core – Anti-Malware Vendors](https://www.opswat.com/docs/mdcore/metascan-engines/anti-malware-vendors)

### [**2. File Type Engine**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-ai-powered-components-in-metadefender-core-#2-file-type-engine)

The File Type Engine can apply AI-enhanced text-based detection models to strengthen file classification accuracy — for example, when analyzing documents or scripts.

This AI-based enhancement is **disabled by default** and can be enabled for environments requiring higher precision in text content recognition.

### [3. **Proactive DLP**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-ai-powered-components-in-metadefender-core-#3-proactive-dlp)

The Proactive Data Loss Prevention (DLP) component applies AI models to identify and classify sensitive or inappropriate content in documents. Key AI-assisted capabilities include:

- **Document identification** (e.g., business, personal, confidential)
- **Detection of “not suitable for work” content**
- **PII (Personally Identifiable Information) detection**

These AI models improve detection accuracy and context awareness beyond traditional keyword or rule-based approaches.

### [4. **Adaptive Sandbox**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-ai-powered-components-in-metadefender-core-#4-adaptive-sandbox)

The Adaptive Sandbox uses AI-driven analysis to interpret behavioural patterns and generate enriched threat intelligence. Examples of AI-powered features include:

- **Executive Summary Generation** – Automatically produces a human-readable summary of observed behavior.
- **Phishing Detection** – Identifies suspicious document or email patterns using machine-learning classifiers.
- **Remote Sandbox Integration** – Some advanced AI features are available only when connected to a standalone **remote sandbox** environment.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
