<!-- source: https://www.opswat.com/docs/filescan/datasheet/hidden-artifact-extraction -->

# Hidden Artifact Extraction

This feature allows the sandbox to reveal hidden artifacts embedded within PE files. Malicious artifacts are often **encoded and/or encrypted** to evade detection and obscure the sample's true intent. Uncovering these artifacts is essential, as they typically contain critical data, such as C2 information or payloads. By extracting them, the sandbox can perform a deeper scan, increasing the likelihood of identifying valuable IOCs.

## [PE Resource XOR Decryption](/docs/filescan/datasheet/hidden-artifact-extraction#pe-resource-xor-decryption)

Storing payloads in PE resources helps malware evade detection by static analysis tools. Many security tools focus on analyzing the executable’s main code section, while resources are often overlooked, making it easier to hide malicious content.

Why XOR encryption? It is widely used for its simplicity and efficiency in evading detection, but one key property of XOR is that when a bit is XORed with 0, the original bit remains unchanged. This characteristic makes XOR encryption particularly "weak" when applied to data with a large number of null bytes, such as those often found in PE files. By analyzing patterns in the encrypted data, especially in areas with many null bytes, the encryption key can be revealed, allowing to decrypt the hidden.

Encrypted Payload Extraction

This sample is a malware loader that contains a encrypted payload in a resource.

On the following link you can find the sample from the screenshot below:

<https://www.filescan.io/uploads/66ab4c2e78d5c73fb1ca7f90/reports/eec0ead1-4ba2-4d6d-acf3-8ca73f9bec6f>

## [Base64-encoded embedded files](/docs/filescan/datasheet/hidden-artifact-extraction#base64-encoded-embedded-files)

Malicious actors embed base64-encoded content, such as executables, archives, or documents within seemingly benign text-based or document files, using them as decoys to evade detection. A more advanced observed evasion technique involves reversing base64-encoded content to bypass detection mechanisms.

MetaDefender Sandbox identifies these potentially malicious embedded files, extracts them, and analyzes their true functionality.

Encoded Payload Extraction

The following sample shows a malicious .NET DLL embedded as a base64-encoded string within an image file

<https://www.filescan.io/uploads/682b0a0ac609634bd7c8e2eb/reports/25a80656-17eb-40a3-beb7-4f80797cf1a3/overview>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
