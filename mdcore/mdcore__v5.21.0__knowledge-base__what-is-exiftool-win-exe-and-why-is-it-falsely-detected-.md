<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-is-exiftool-win-exe-and-why-is-it-falsely-detected- -->

# What Is exiftool_win.exe and Why Is It Falsely Detected?

**Overview**

When the **Exif feature** is enabled in **MetaDefender Core’s Filetype engine settings**, customers may notice the presence of the executable **exiftool*win.exe*** *under the Core resource directory (e.g., data\resources\filetype* 15_windows_<ID>\exif_cache_<ID>).

This file may be flagged by certain antivirus engines as a potential threat due to its unsigned status and self-extracting behavior.

This article explains why exiftool_win.exe exists, how it behaves, and what can be done to manage false positive detections.

**Why Is exiftool_win.exe Present?**

exiftool_win.exe is a **third-party utility** integrated into MetaDefender Core to extract metadata from files. It is a core component of the Exif processing functionality.

- **Tool Origin:** ExifTool is an open-source utility developed by Phil Harvey, widely used for reading and writing metadata.
- **Windows Packaging:** On Windows, ExifTool is distributed as a **self-extracting Perl executable**. When run:
- It extracts embedded Perl scripts to a **temporary folder**.
- This temporary location is defined during engine initialization by MetaDefender Core.

Example of the folder path:

C:\Program Files\OPSWAT\MetaDefender Core\data\resources\filetype_15_windows_\exif_cache_

**Why Is It Flagged by Antivirus Software?**

Some antivirus (AV) engines may detect exiftool_win.exe as malicious for the following reasons:

- **It is not digitally signed** – some AVs treat unsigned executables as suspicious.
- **Heuristic detection** – the self-extraction behavior is commonly seen in malicious droppers or downloaders.
- **False positive patterns** – occasionally, the hash or behavior matches known malware patterns erroneously.

Example:

- A customer reported detection as TrojanDownloader.Banload.btij by two AV engines on VirusTotal.
- Hash of the file in question:
- **SHA256**: 190fa21bca88e2c4ac0ebea467be79f2fda63ccd45915d72a2582ca30a3c7c67

**What Can Be Done About It?**

✅ Recommended Actions:

1. **Report False Positives:**

   1. Report the detection to the affected AV vendors.
   2. One vendor (Zillya) confirmed it as a false positive and resolved it in a database update.
2. **Allowlist MetaDefender Core Folder:**

   1. If real-time protection (RTP) is enabled on the server, we recommend allowlisting the **entire MetaDefender Core installation directory**, e.g.:

C:\Program Files\OPSWAT\MetaDefender Core\

1. **Monitor & Communicate**:

   1. This behavior is expected and known. Inform customers and security teams as necessary.
   2. Refer them to this article or similar documentation to clarify the usage and behavior of the file.
