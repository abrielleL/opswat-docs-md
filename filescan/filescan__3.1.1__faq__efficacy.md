<!-- source: https://www.opswat.com/docs/filescan/3.1.1/faq/efficacy -->

# How good is the efficacy for in-the-wild malware?

Currently, our in-the-wild efficacy for malicious office files ("maldocs") is 90%+ (and growing). This means, our sandbox engine achieves the same result as a full-blown virtualization based sandbox (including bypasses for anti-analysis, sleep tricks, and environment checks) in a fraction of time. Besides emulators for VBA macros, we offer emulation of javascript, vbscript, powershell and more. See a full list of supported file types here: [Supported File Types](/datasheet/supported-file-types).

For PE support, **MetaDefender Aether** implements generic unpackers and full binary analysis with automated code extraction & analysis using diassemblers and symbol annotation.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
