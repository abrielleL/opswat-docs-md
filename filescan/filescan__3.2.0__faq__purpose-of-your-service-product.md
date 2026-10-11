<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/purpose-of-your-service-product -->

# Why use MetaDefender Aether?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The primary focus of **MetaDefender Aether** (previously known as MetaDefender Sandbox) and its standalone edition is not only to detect malicious files, but also to extract potential "Indicators of Compromise" (IOCs) from compressed, obfuscated, and encrypted data in a short time and without full runtime analysis that requires a slow and resource-intensive virtual machine (VM). This process is performed using a set of proprietary emulation engines (including virtual file systems and partial OS emulation), at scale and with rapid speed compared to traditional VM-based runtime analysis.

For example, an email (msg/eml) with a maldoc attachment (typically containing a heavily obfuscated VBA macro) is fully analyzed within ~10-15 seconds including all relevant threat indicators. This includes inspection of download URLs, underlying files, as well as a recursive analysis of embedded artifacts.

In addition, all files are scanned for thousands of malicious threats and – when possible – mapped to the MITRE ATT&CK framework for quicker assessment. Using generative AI, an easy digestable executive summary can be generate for your analysts.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
