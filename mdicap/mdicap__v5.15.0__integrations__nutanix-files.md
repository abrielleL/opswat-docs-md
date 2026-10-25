<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/nutanix-files -->

# Nutanix Files

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdicap/v5.15.0/integrations/nutanix-files#overview)

Nutanix Files supports the Internet Content Adaptation Protocol (ICAP) to enable communication with MetaDefender ICAP Server. ICAP Server can scan files stored on file shares in real time when files are opened, closed, read from, or written to.

Nutanix Files performs the following task when working with ICAP Server:

1. A client requests to read, write, open, or close a file.
2. Files determines that the file requires scanning.
3. Files sends files that require scans to the ICAP Server and with a scan request.
4. The ICAP Server scans the file and reports the scan results to Files.
5. Files quarantines and denies access to unsafe files.
6. If the file is clean or [disarmed & reconstructed](https://www.opswat.com/technologies/data-sanitization), then Files allows the client access to the file.

Info

For details about ICAP Server configuration in Nutanix Files see the [Nutanix Files Guide](https://portal.nutanix.com/page/documents/details/?targetId=Files-v35:Files-v35).

## [Configuration](/docs/mdicap/v5.15.0/integrations/nutanix-files#configuration)

Info

By default, shares have antivirus scan disabled. After configuring the antivirus scan, you must enable the scan for each share that you want scanned.

Info

Nutanix recommends two or more MetaDefender ICAP Servers for each share.

## [Configure scanning](/docs/mdicap/v5.15.0/integrations/nutanix-files#configure-scanning)

To configure scanning for SMB shares:

1. Log on to the Prism web console and go to *Home > File Server*.
2. In the action links, click *Antivirus settings*. The *Antivirus* window appears.
3. Click *+ Connect ICAP Server*

1. Enter the IP address or hostname of ICAP Server.

2. Enter the ICAP Server port number. The default port is 1344.

3. Click *Save*.

4. Ensure the connection status automatically updates to *OK*. For a detected antivirus server, the software tests the validity of the configured server and updates the status to *OK*. [012ec5a8-8168-4a71-aec3-b75f584cacce](https://onlinehelp.opswat.com/icap/attachments_4864452_1_012ec5a8-8168-4a71-aec3-b75f584cacce)

5. Click *Next*.

Complete the *Scan Settings*. Override settings for individual shares through the share-level antivirus settings. *Scan on Write*: Scans saved and updated files (a write operation)._

- Scan on Read: Scans opened files (read operation).Nutanix recommends to always enable *Scan on Read*.
- Click *Save*.

_

## [Enable scanning](/docs/mdicap/v5.15.0/integrations/nutanix-files#enable-scanning)

Info

By default, shares have antivirus scan disabled.

To enable scanning on each share:

1. From the *Home* page, go to *File Server > Share*.
2. Select the share from the list and click *Antivirus Settings*. The antivirus setup window displays.
3. Check the box *Enable antivirus scan for this share*.
4. Click *Save*.
