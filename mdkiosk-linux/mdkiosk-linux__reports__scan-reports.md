<!-- source: https://www.opswat.com/docs/mdkiosk-linux/reports/scan-reports -->

# Scan Reports

Scan Reports are generated after Kiosk finishes scanning the media.

These reports are uploaded to the management server and are available in three different formats: `JSON`, `PDF`, & `TXT`.

### [**JSON**](/docs/mdkiosk-linux/reports/scan-reports#json)

The `JSON` report is the full report from Kiosk. This format provides all of the information from the media scan, however this format is not very human-readable and is intended to be used in a JSON parser to access specific information. A full breakdown of the attributes in this report is found on the next page, [Report Schema](https://docs.opswat.com/mdkiosk-linux/reports/report-schema).

### [**PDF and TXT**](/docs/mdkiosk-linux/reports/scan-reports#pdf-and-txt)

The `PDF` and `TXT` reports are summaries of the information found in the JSON reports. These reports provide a brief summary of the file totals for scan results, and then lists out the file paths and a SHA256 hash for files that did not return with a `No Threat Detected` result. For example:
