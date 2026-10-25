<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/process/scan---results -->

# Scan Reports

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Drive offers comprehensive scan reports with detailed lists of issues and vulnerabilities found during scans. Once a scan is completed and its report is generated, users can view lists of the **Files with no issues**, **Potentially Infected files**, **Files with** **Potential Zero-Day Vulnerabilities**, **Files with Sensitive Data**, **Files with Suspicious** **Country of Origin**, and **Skipped Files**. And along with that, previous scan reports can be accessed from the **Reports** page.

### [Potentially Infected](/docs/mddrive/v4.4.10/process/scan---results#potentially-infected)

Includes a list of files with potential malware infection:

### [Potentially Vulnerable Files](/docs/mddrive/v4.4.10/process/scan---results#potentially-vulnerable-files)

Includes a list of files with potential vulnerabilities that are suspected to be a cause of a Zero-Day attack:

### [Sensitive Data](/docs/mddrive/v4.4.10/process/scan---results#sensitive-data)

Includes a list of files with detected sensitive data, such as passwords and private keys:

### [Country of Origin](/docs/mddrive/v4.4.10/process/scan---results#country-of-origin)

Includes a list of files with non-compliant country of origin. You can [set the list of non-compliant countries](https://www.opswat.com/docs/mddrive/configuration/preferences---country-of-origin) from **Settings** → **Preferences**.

### [Integrity Failures](/docs/mddrive/v4.4.10/process/scan---results#integrity-failures)

Integrity failures are detected when a baseline is set for a workflow. In that case, when you select **Rerun** from the Workflow page or **Run this scan again** from the Reports page, MetaDefender Drive will compare every single file in the scanned path associated with the selected workflow to their baseline. The **Integrity Failure** result will include details of the differences found. You can learn more about workflows on the [Using Workflows](https://docs.opswat.com/mddrive/process/processing-workflows) page.

New and modified files detected after comparing the scan results to the baseline

Detected a file that was modified with sensitive data after comparing it to the baseline report

### [Boot Sector Infections](/docs/mddrive/v4.4.10/process/scan---results#boot-sector-infections)

Includes the system partitions infected by boot sector malware.

Warning

It is advised not to boot the system if a boot sector malware was detected. The recommended action is to format the disk or perform OS and applications data recovery from a full-image backup or a restore point.

Boot sector infection detected

### [Firmware (BIOS/UEFI) Vulnerabilities](/docs/mddrive/v4.4.10/process/scan---results#firmware-biosuefi-vulnerabilities)

Includes a list of the detected firmware vulnerabilities that could make your device vulnerable to RootKit attacks.

Info

In case of a firmware vulnerability detection, MetaDefender Drive will provide details about the last time your system's firmware was upgraded if a more recent version of the firmware is available, and the CVEs that might be present in the current version.

Details of a firmware vulnerability

Firmware Updates

OPSWAT maintains a database of firmware upgrades and keeps it updated periodically with each release. If you find a mismatch or outdated information, please contact OPSWAT with detailed information about the system.

## [System Properties](/docs/mddrive/v4.4.10/process/scan---results#system-properties)

By clicking the **View Properties** button at the top of the scan results page, you will be able to view properties extracted from the scanned system, including Serial Number, CPU, Memory, Hostname, Operating System, IP address, and MAC address.

System Properties window

### [Saving Report Files](/docs/mddrive/v4.4.10/process/scan---results#saving-report-files)

After each scan, the report will be saved in the ***/reports*** folder of MetaDefender Drive's NTFS partition. From **Settings** →**Preferences** → **Reports,** **you can choose to save the scan reports** **in the following formats:** JSON (default), TXT, PDF and CSV.

Report saving formats

Info

Saving reports to external media is recommended to ensure no data is lost in case of a MetaDefender Drive malfunction.

To view more details about **Skipped Files** and to manage **Scan Results**, please see:

- [Skipped Files in Results](/docs/mddrive/v4.4.10/process/skipped--files)
- [Results Management](/docs/mddrive/v4.4.10/process/results--management)
