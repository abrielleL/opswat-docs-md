<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/steganography-analysis -->

# Image Steganography Analysis

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Threat actors use steganography to hide malware by embedding malicious data within seemingly harmless files — most often images.

Common stego techniques in malware include:

- Appending encoded data at the end of image files.
- Hiding payloads in image metadata.
- Image header spoofing — e.g., mimicking a BMP header for shellcode delivery.

These images are then used to deliver shellcode, stage payloads, or backdoors — often bypassing static detection due to their valid format and benign appearance.

### [Base64-Encoded PE Files Appended to Images for Payload Delivery](/docs/filescan/3.2.0/datasheet/steganography-analysis#base64-encoded-pe-files-appended-to-images-for-payload-delivery)

Threat actors conceal malicious payloads by encoding PE files in Base64 and appending them to valid image files — typically JPG or PNG. These images remain visually intact and functional, allowing them to bypass basic file-type detection and evade suspicion. To further hinder detection, attackers often reverse the Base64 string, making static analysis more difficult.

In recent campaigns, stegomalware has leveraged images to distribute infostealers. The sample under analysis is a JPG file containing a reversed Base64-encoded PE. MetaDefender Sandbox detected the anomaly, extracted and decoded the payload, and identified it as AgentTesla, a well-known .NET-based infostealer. Further analysis uncovered encrypted strings and C2 configuration data, enabling attribution and mapping of the malware’s command-and-control infrastructure.

Sandbox Report

<https://www.filescan.io/uploads/689366b16d7bffa0a79f16f6/reports/6c4b2383-6be0-41ba-9f71-e91920715d2b/overview>

### [PNG Metadata Abuse to Embed a Malicious Script](/docs/filescan/3.2.0/datasheet/steganography-analysis#png-metadata-abuse-to-embed-a-malicious-script)

Threat actors abuse image metadata fields to deliver and execute malware. These fields are often overlooked by security tools, making them a stealthy channel for malicious activity.

In this observed case, a PNG image contains an embedded command within its metadata that fetches and executes a remote PHP web shell hosted on GitHub. The payload is retrieved and executed on the host — effectively turning an innocent-looking image into a web-based loader. The use of trusted infrastructure and obfuscated code hidden in metadata enables attackers to bypass traditional static detection.

MetaDefender Sandbox successfully flagged the malicious script and identified the next-stage URL, revealing the underlying infrastructure and enabling further analysis.

Sandbox Report

<https://www.filescan.io/uploads/684496f4fd02ed5e059d72c5/reports/bf40f1e3-2fdf-4383-9da9-4d49e9fd658a/overview>

### [BMP Header Spoofing to Deliver Shellcode](/docs/filescan/3.2.0/datasheet/steganography-analysis#bmp-header-spoofing-to-deliver-shellcode)

Threat actors abuse image formats to embed directly a shellcode. In this case, the BMP file contains a jump instruction (JMP) in place of the standard header, mimicking the BM signature used in valid BMP images. This allows the sample to masquerade as a legitimate image while being loaded and executed as shellcode.

This shellcode follows a polymorphic decrypt-and-execute stub: it first scans for a known marker, then XOR-decrypts the embedded payload, and finally jumps to execute it in memory. This technique enables covert shellcode delivery under the guise of an image — often bypassing static detection and misleading analysts during triage.

MetaDefender Sandbox detects this early-stage masquerading, extracts the shellcode within the spoofed BMP container— enabling analysts to proceed with in-depth shellcode analysis.

Sandbox Report

<https://www.filescan.io/uploads/66bc890f32f6d05ff3ccc70f/reports/09c00ac0-a82c-42ea-8940-e61b62e71ada/overview>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
