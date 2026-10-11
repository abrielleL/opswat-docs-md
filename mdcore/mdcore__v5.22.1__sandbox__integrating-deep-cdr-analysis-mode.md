<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/sandbox/integrating-deep-cdr-analysis-mode -->

# Enhancing Threat Detection with Deep CDR & MetaDefender Aether for Core (Adaptive Sandbox)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check your version

This article applies to MetaDefender Core 5.12.1 (or higher) and Adaptive Sandbox 2.1.0 (or higher) releases deployed on Windows or Linux systems.

Integrating Deep CDR Analysis Mode with Adaptive Sandbox provides a layered approach to security, combining content disarmament (CDR) for immediate risk reduction with sandbox analysis for advanced zero-day detection.

- **Deep CDR acts as a pre-filter** by stripping active content (e.g., macros, scripts) to mitigate risk but does **not** determine if the file was malicious.
- **Adaptive Sandbox is required for full threat analysis**, identifying **zero-day threats, hidden malware, and evasive techniques** that CDR alone cannot detect.
- **Using CDR to trigger sandboxing** ensures that high-risk files (those containing active content) are analyzed more deeply while reducing unnecessary sandbox scans for benign files.

### **I. Why This Matters**

Stripping active content is a foundational step in securing a file. If a file was originally malicious, removing certain elements merely disarms the malicious content, **its inherent untrustworthiness remains.**

Sandbox analysis complements CDR to uncover the true threat and potential scale of an attack, allowing for a **deeper inspection of Obfuscation, Behavioral Patterns and the identification of unknown malware.**

## II. How to setup

Files are routed to the Sandbox based on multiple independent filters. A file that matches **any** of below filters will be sent Sandbox analysis.

- **Enable for Deep CDR result(s)**
- **Enable for Active Content(s) found by DeepCDR**

### 1. Setup Deep CDR Analysis mode

If you prefer to retain your files without modifications while still leveraging the benefits of CDR integration, enable the **CDR Analysis Mode**. For more information, visit the Deep CDR [analysis mode page](https://www.opswat.com/docs/mdcore/deep-cdr/analysis-mode).

#### Enable Deep CDR for archives

To submit archives for processing, ensure that **Deep CDR Archive Processing** is enabled in the **Archive Compression Engine Workflow Settings**. Additionally, activate the required archive types for your use case. For detailed instructions, refer to the Deep CDR [advanced configuration page](https://www.opswat.com/docs/mdcore/deep-cdr/advanced-configurations).

### 2. Setup Active Content trigger

Under **Workflow Management** -> **Workflows** -> **(Name of the workflow)** -> **Adaptive Sandbox** -> **Advanced configuration** There is an option "Enable for Active Content(s) found by Deep CDR":

When enabled and specific active content types are selected, files in which Deep CDR detects those types (e.g., JavaScript, scripts, embedded objects) are automatically routed to the Sandbox.

****Note****: In Analysis Mode, Deep CDR does not generate sanitized files. As a result, the Deep CDR result will always be “Sanitization skipped” or “No Specific Configuration” (for unsupported file types). To prevent unnecessary files from being sent to the Sandbox, remove “Sanitization skipped” and “No Specific Configuration” from the **Enable for Active Content(s) found by Deep CDR** filter.

## III. Example configurations

With below configurations:

Although Deep CDR detected active content, no sanitized file was generated because the system was running in **CDR Analysis Mode**. The final verdict was determined by **Adaptive Sandbox**, which identified malicious behavior and blocked the file.

In the example below, the CSV file does not contain active content. As a result, Deep CDR reported **“Sanitization skipped”** with no findings, and **Adaptive Sandbox** was skipped because no execution triggers were detected.

## IV. Key Takeaway

Deep CDR **removes risky elements but does not determine trustworthiness**—it is not a replacement for threat detection. **Adaptive Sandbox is required to detect malware and unknown threats, ensuring true zero-trust security.**

Support

If **Further Assistance** is required, please follow the instructions on [How To Create a Support Package](https://docs.opswat.com/mdcore/troubleshooting/how-to-create-support-package-), then proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support-services).
