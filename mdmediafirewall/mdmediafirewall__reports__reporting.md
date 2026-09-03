<!-- source: https://www.opswat.com/docs/mdmediafirewall/reports/reporting -->

# Reporting

When Media Firewall finishes scanning media, it will generate multiple reports of the scanning session at the root of the drive displayed on the host system.

## [Activity Log](/docs/mdmediafirewall/reports/reporting#activity-log)

The `session-activity-log.txt` is a quick look into the scan session showing the progress of the session, files currently being looked at and running counts of the file categories. Each log line is timestamped for accurate tracking.

The activity log only contains information on the current session ran.

2023-09-25T20:41:25Z: Scan started on device USB-A
2023-09-25T20:41:25Z: Progress 0% (Allowed: 0; Blocked: 0; Concealed: 0)
2023-09-25T20:41:25Z: Looking into /media/Disk1/DLP/corrupted.xlsx
2023-09-25T20:41:25Z: Error: File not found in Media Manifest.
2023-09-25T20:41:25Z: Progress 5% (Allowed: 0; Blocked: 0; Concealed: 1)
2023-09-15T20:41:25Z: Looking into /media/Disk1/eicar.com
2023-09-15T20:41:25Z: Progress 26% (Allowed: 3; Blocked: 1; Concealed: 1)
2023-09-15T20:41:25Z: Looking into /media/Disk1/CDR/scan_file.pdf
2023-09-15T20:41:25Z: Progress 47% (Allowed: 7; Blocked: 1; Concealed: 1)
2023-09-15T20:41:25Z: Looking into /media/Disk1/DLP/DOC/sample.docx
2023-09-15T20:41:25Z: Progress 74% (Allowed: 12; Blocked: 1; Concealed: 1)
2023-09-15T20:41:25Z: Looking into /media/Disk1/DLP/clean.html
2023-09-15T20:41:25Z: Progress 95% (Allowed: 16; Blocked: 1; Concealed: 1)
2023-09-15T20:41:26Z: Scan finished 100% - Total time: 00:00:01

---

## [Session Report](/docs/mdmediafirewall/reports/reporting#session-report)

### [JSON](/docs/mdmediafirewall/reports/reporting#json)

The `session-report.json` is the full report from Media Firewall. This format provides all of the information from the media scan and is intended to be used with a JSON parser to access specific information. A full breakdown of the attributes in this report is found on the next page, [Report Schema](https://docs.opswat.com/mdmediafirewall/reports/report-schema).

### [TXT](/docs/mdmediafirewall/reports/reporting#txt)

The `session-report.txt` is a formatted report that provides a brief summary of the file totals for scan results and lists out the file paths and a SHA256 hash for files.

---

## [Stored Reports in Central Management](/docs/mdmediafirewall/reports/reporting#stored-reports-in-central-management)

When connected to Central Management, Media Firewall will upload the JSON report after finishing scanning media.

The session report in Central Management is available in three different formats: `JSON`, `PDF`, & `TXT`.

All the information is similar to the session reports that can be temporarily viewed on the Host system.

Info

Media Firewall does not maintain a local history of reports. Local reports are only available on the Host while the media is connected. A connection to Central Management is required to view reports from past sessions.
