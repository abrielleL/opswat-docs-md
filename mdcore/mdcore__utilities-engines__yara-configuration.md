<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/yara-configuration -->

# Configuration

### [Enable Adaptive Sandbox rules](/docs/mdcore/utilities-engines/yara-configuration#enable-adaptive-sandbox-rules)

The following option can be used to enable Adaptive Sandbox curated rules to identify the most common attack vectors. These rules are only used to find potentially malicious PE files, not meant to be used as a blocklist.

#### [Result with Sandbox rule](/docs/mdcore/utilities-engines/yara-configuration#result-with-sandbox-rule)

Info

Starting from Core version 5.14.0 and Adaptive Sandbox 2.3.0, these rules can be used to trigger Sandbox scans based on the results.
