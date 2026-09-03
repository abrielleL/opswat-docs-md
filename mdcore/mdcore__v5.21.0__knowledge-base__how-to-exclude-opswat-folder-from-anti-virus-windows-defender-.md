<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-exclude-opswat-folder-from-anti-virus-windows-defender- -->

# How to exclude OPSWAT folder from Anti-Virus Windows Defender?

This article applies to all MetaDefender Core V5 releases deployed on Windows systems.

When scanning sample malware files, such as the commonly used EICAR from [Download Anti Malware Testfile - EICAR](https://www.eicar.org/download-anti-malware-testfile/), it is important to exclude the OPSWAT folder from **all** existing Anti-Virus software programs on the machine. Failure to exclude the OPSWAT folder can lead to “Not Scanned” results, as the Anti-Virus software will pick up the malware signatures for processing before the MetaDefender Core software can process. Therefore, MetaDefender Core will be unable to determine the hash, leading to the scan result “Not Scanned”.

Common Anti-Virus softwares to perform exclusions, including but not limited to: McAfee, Norton, Bitdefender, Malwarebytes, SentinelOne

### [How to exclude on Windows Defender](/docs/mdcore/v5.21.0/knowledge-base/how-to-exclude-opswat-folder-from-anti-virus-windows-defender-#how-to-exclude-on-windows-defender)

Please ensure you have the proper permissions to add exclusions, such as administrator rights.

1. Navigate to “Windows Security” > “Virus & threat protection”

2. Under “Virus & threat protection settings” click “Manage settings”

3. Scroll down to “Exclusions” and click “Add or remove exclusions”

4. Add the folder “OPSWAT”, by default it is located in the install directory: "C:\Program Files\OPSWAT" [Your directory may be different depending on if you have performed a customer install, placing the OPSWAT folder inside a separate Drive]
5. Add the folder “Temp” stored at location `C:\Users\<user>\AppData\Local\Temp`.

**Important Note regarding engine process exclusion**

Important:

- If Windows Defender is used **only** as a local AV (and **not** as an AV engine inside MetaDefender Core), then you **may** additionally exclude these MetaDefender Core processes: `engineprocess.exe`, `engineprocess32.exe`, `ometascan.exe`, `postgres.exe`, and `nginx.exe`.
- However, if Windows Defender is configured **both** as the local AV **and** as an AV engine inside MetaDefender Core, then you **should not exclude** `engineprocess.exe` (and its variant) from the real-time protection exclusion list. Excluding the engine process in that scenario can impair the integrated AV engine’s functionality.

**Registry Exclusion (Optional)**

You can optionally exclude the following registry path:

`HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global`

For the values: `dlppath`, `quarantinepath`, `sanitizepath`.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
