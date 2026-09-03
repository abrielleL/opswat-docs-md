<!-- source: https://www.opswat.com/docs/mdkiosk-linux/reports/report-schema -->

# Report Schema

Here you will find an explanation of the `JSON` report schema

### [**allowed**](/docs/mdkiosk-linux/reports/report-schema#allowed)

- file_paths: JSON array of files with Allowed result

ExampleCopy"allowed": {
"file_paths": [
"/media/Disk2/MD4M_Test_USB/3mb.zip",
"/media/Disk2/MD4M_Test_USB/1mb.zip",
"/media/Disk2/MD4M_Test_USB/2mb.zip"
]
}

---

### [**av_info**](/docs/mdkiosk-linux/reports/report-schema#av_info)

JSON object containing objects describing the scanning engines used

- key is the name of AV engine

  - def_time: timestamp of the last time the engine was updated
  - eng_id: string used to identify the engine

ExampleCopy"av_info": {
"Ahnlab": {
"def_time": "2021-09-21T00:00:00.000Z",
"eng_id": "ahnlab_1_linux"
},
"Avira": {
"def_time": "2021-09-20T11:43:00.000Z",
"eng_id": "avira_1_linux"
},
"Bitdefender": {
"def_time": "2021-09-20T11:20:57.000Z",
"eng_id": "bitdefender_1_linux"
}
}

---

### [**blocked**](/docs/mdkiosk-linux/reports/report-schema#blocked)

- file_paths: JSON array of file paths with Blocked result

---

### [**cdr**](/docs/mdkiosk-linux/reports/report-schema#cdr)

- file_paths: JSON array of files with Zero-Day Protection results

---

### [**coo**](/docs/mdkiosk-linux/reports/report-schema#coo)

- file_paths: JSON array of files blocked due to Country Of Origin

---

### [**copy_info**](/docs/mdkiosk-linux/reports/report-schema#copy_info)

`optional` displays when a `Scan and Copy` workflow was used

- total_failures: count of how many files failed to copy
- total_processed: count of sanitized and redacted files successfully copied
- total_unprocessed: count of files copied that were not sanitized or redacted

---

### [**cve**](/docs/mdkiosk-linux/reports/report-schema#cve)

JSON object containing objects that describe Vulnerability findings

- key is the name of the CVE ID from the [National Vulnerability Database](nvd.nist.gov)

  - access_complexity: a CVSS access-complexity descriptor
  - access_vector: a CVSS access-vector descriptor
  - authentication: a CVSS authentication descriptor
  - description: a text description of the specific vulnerability
  - file_paths: JSON array of files with this CVE result
  - impact: JSON object describing impact description

    - availability: a CVSS availability impact descriptor
    - confidentiality: a CVSS confidentiality impact descriptor
    - integrity: a CVSS integrity impact descriptor
  - last_modified_time: last modified time for this CVE
  - published_time: last published time for this CVE
  - severity: String description of Severity level:

    - `LOW`
    - `MODERATE`
    - `IMPORTANT`
    - `CRITICAL`
    - `NOT_AVAILABLE`
    - `UNKNOWN`
  - severity_index: 5 point scale numerical description of Severity level with 5 being greatest and 0 being unknown

ExampleCopy"cve": {
"CVE-2016-1038": {
"access_complexity": "LOW",
"access_vector": "NETWORK",
"authentication": "NONE",
"description": "Adobe Reader and Acrobat before 11.0.16, Acrobat and Acrobat Reader DC Classic before 15.006.30172, and Acrobat and Acrobat Reader DC Continuous before 15.016.20039 on Windows and OS X allow attackers to bypass JavaScript API execution restrictions via unspecified vectors, a different vulnerability than CVE-2016-1039, CVE-2016-1040, CVE-2016-1041, CVE-2016-1042, CVE-2016-1044, CVE-2016-1062, and CVE-2016-1117.",
"file_paths": [
"/media/Disk8/COO_usa/vulnerable_file.exe"
],
"impact": {
"availability": "COMPLETE",
"confidentiality": "COMPLETE",
"integrity": ""
},
"last_modified_time": "2016-12-01T03:03:00Z",
"published_time": "2016-05-11T10:59:00Z",
"severity": "CRITICAL",
"severity_index": 81
}
}

---

### [**end_time**](/docs/mdkiosk-linux/reports/report-schema#end_time)

scan end timestamp

---

### [**infected**](/docs/mdkiosk-linux/reports/report-schema#infected)

- file_paths: JSON array of infected file paths

---

### [**name**](/docs/mdkiosk-linux/reports/report-schema#name)

name for this specific report made from internal instance ID, date, and time

---

### [**paths**](/docs/mdkiosk-linux/reports/report-schema#paths)

JSON array of mount points for scanned media

---

### [**result_set**](/docs/mdkiosk-linux/reports/report-schema#result_set)

JSON object containing objects for individual file results

- key is the full path to the file

  - **av_info**: JSON object containing objects describing results from scanning engine

    - key is AV name

      - **scan_result_i**: (internal use only)
      - **threat_found**: optional, only included if engine returns an infected result
      - **engine_result**: result from the scanning engine
  - **cdr_info**: *null* or a JSON object describing Zero-Day scan results for this file

    - **description**: string with CDR engine result
    - **details**: JSON array containing objects describing actions taken by the CDR engine (optional, could be empty)

      - **action**: string for action taken by CDR engine
      - **object_name**: string for type of object sanitized
    - **sanitized_file_inf**o: JSON object with information about the available sanitized file

      - **file_size**: size of sanitized file
      - **sha256**: sha256 hash of the sanitized file
  - **coo_info**: *null* or JSON object containing Country Of Origin information

    - **company_name**: name of company that created this file
    - **country_of_origin**: location where this file was created
    - **violates_policy**: boolean for whether or not this file violates the policy set in the Kiosk settings
  - **cve_info**: JSON array containing the CVE IDs of all CVEs found in this file
  - **dlp_info**: JSON object containing Data Loss Prevention engine results

    - **hits**: *null* or object containing DLP hit details

      - **ssn**: (optional) object describing Social Security Number hits

        - **display_name**: display name for this type of hit
        - **hits**: JSON array of objects describing each SSN hit
      - **ccn**: (optional) object describing Credit Card Number hits

        - **display_name**: display name for this type of hit
        - **hits**: JSON array of objects describing each CCN hit
  - **extraction_info**: JSON object containing information about any files extracted from this file. This will be empty for any non-archive file
  - **file_info**: JSON object containing details about this file

    - **display_name**: display name for this file
    - **file_size**: size of file
    - **file_type**: technical name for type of file
    - **file_type_description**: simple name for type of file
    - **md5**: MD5 hash of file
    - **sha1**: SHA1 hash of file
    - **sha256**: SHA256 hash of file
  - **primary_result**: the overall scan result determined from all engine results
  - **removed**: boolean for whether the infected file was deleted
  - **transfer_info**: JSON object containing details on where the file was copied to

ExampleCopy"result_set": {
"/media/Disk1/eicar.com": {
"av_info": {
"Ahnlab": {
"scan_result_i": 1,
"threat_found": "Virus/EICAR_Test_File"
},
"Avira": {
"scan_result_i": 1,
"threat_found": "Eicar-Test-Signature"
}
},
"cdr_info": null,
"coo_info": null,
"cve_info": {
"cve": []
},
"dlp_info": {
"hits": null
},
"extraction_info": {},
"file_info": {
"display_name": "eicar.com",
"file_size": 68,
"file_type": "application/octet-stream",
"file_type_description": "EICAR virus test files",
"md5": "44d88612fea8a8f36de82e1278abb02f",
"sha1": "3395856ce81f2b7382dee72602f798b642f14140",
"sha256": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
},
"primary_result": "Infected"
},
"/media/Disk1/ri.docx": {
"av_info": {
"Ahnlab": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
},
"Avira": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
}
},
"cdr_info": {
"description": "Sanitized successfully.",
"details": [
{
"action": "removed",
"count": 1,
"object_name": "OLE"
},
{
"action": "sanitized",
"object_name": "XML content"
}
],
"sanitized_file_info": {
"file_size": 10713,
"sha256": "9ef0a41cc2a8489a5d6ecc6ad15e8e5f83509f1c41fa89e81669735585eb2808"
}
},
"coo_info": null,
"cve_info": {
"cve": []
},
"dlp_info": {
"hits": {
"ssn": {
"display_name": "Social Security Number",
"hits": [
{
"after": "",
"before": "test file Hook: https://webhook.site/#/dc9c7bfa-9cf7-40a9-90e9-a25e89fb6937/3315680a-35b2-4a5b-bb90-dfc550109c70/0 SSN:",
"certainty": "High",
"certainty_score": 88,
"hit": "XXXXXXX2345",
"location": "Page 1",
"severity": 0,
"tryRedact": true
}
]
}
}
},
"extraction_info": {},
"file_info": {
"display_name": "ri.docx",
"file_size": 12662,
"file_type": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
"file_type_description": "Microsoft Word Document",
"md5": "0a5af08976219fb9038c8745ca2a60b0",
"sha1": "fa15378170dd319ccb43689cc3e45aed54908386",
"sha256": "045dc650a6f2028b63a0e7102318b35ab42af335f3bdd2168342fc4f11c91897"
},
"primary_result": "No Threat Detected"
}
}
}

---

### [**rootkit_allowed**](/docs/mdkiosk-linux/reports/report-schema#rootkit_allowed)

- file_paths: JSON array of scanned boot sector files with Allowed result

---

### [**rootkit_blocked**](/docs/mdkiosk-linux/reports/report-schema#rootkit_blocked)

- file_paths: JSON array of scanned boot sector files with Blocked result

---

### [**session_error**](/docs/mdkiosk-linux/reports/report-schema#session_error)

(optional): a string with an error message.

Only included in report if there was an issue that stopped the session without user interaction

---

### [**session_type**](/docs/mdkiosk-linux/reports/report-schema#session_type)

type of session

- `scan` -> Scan workflow
- `copy` -> Scan and Copy to USB workflow
- `vault` -> Scan and Copy to Managed File Transfer workflow

---

### [**skipped**](/docs/mdkiosk-linux/reports/report-schema#skipped)

- file_paths: JSON array of paths for any files that skipped scanning

---

### [**start_time**](/docs/mdkiosk-linux/reports/report-schema#start_time)

scan start time

---

### [**total_result_count**](/docs/mdkiosk-linux/reports/report-schema#total_result_count)

total count of all files scanned

---

### [**user_question_answer**](/docs/mdkiosk-linux/reports/report-schema#user_question_answer)

JSON array containing objects for questions and answers

- key is text of the question

  - answer: users' answer to the question

---

**uuid:** (internal use only)

**version:** (internal use only)

---

### [**vault_guest**](/docs/mdkiosk-linux/reports/report-schema#vault_guest)

(optional when `Scan and Copy to MetaDefender Managed File Transfer` is enabled)

Guest ID to log into Managed File Transfer to retrieve transferred files

### [**vault_guest_qr_base64**](/docs/mdkiosk-linux/reports/report-schema#vault_guest_qr_base64)

(optional when `Scan and Copy to MetaDefender Managed File Transfer` is enabled, internal use only)

---

## [Example JSON Report](/docs/mdkiosk-linux/reports/report-schema#example-json-report)

ReportCopy{
"allowed": {
"file_paths": [
"//dev/sda//block/0/1",
"//dev/sda1//block/0/1"
]
},
"av_info": {
"Ahnlab": {
"def_time": "2021-10-05T00:00:00.000Z",
"eng_id": "ahnlab_1_linux"
},
"Avira": {
"def_time": "2021-10-04T11:25:00.000Z",
"eng_id": "avira_1_linux"
}
},
"blocked": {
"file_paths": [
"/media/Disk1/ri.docx",
"/media/Disk1/eicar.com"
]
},
"cdr": {
"file_paths": [
"/media/Disk1/ri.docx"
]
},
"coo": {
"file_paths": []
},
"cve": {},
"dlp": {
"file_paths": [
"/media/Disk1/ri.docx"
]
},
"end_time": "2021-10-04T21:43:30Z",
"infected": {
"file_paths": [
"/media/Disk1/eicar.com"
]
},
"name": "MK54c4c454400543010805ac6c04f513733-20211004-214328",
"paths": [
"/media/Disk1/",
"//dev/sda//block/0/1",
"//dev/sda1//block/0/1"
],
"result_set": {
"//dev/sda//block/0/1": {
"av_info": {
"Ahnlab": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
},
"Avira": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
}
},
"cdr_info": null,
"coo_info": null,
"cve_info": {
"cve": []
},
"dlp_info": {
"hits": null
},
"extraction_info": {},
"file_info": {
"display_name": "1",
"file_size": 512,
"file_type": "application/octet-stream",
"file_type_description": "DOS/MBR boot sector",
"md5": "4deed20c2ed05440d847dfc2db1efe62",
"sha1": "8ae87680d4745b0ca90399f942e6a10ed7600142",
"sha256": "a59ed5179435d31c370a37792bf63c5d2dfadc0c20d72ec5092b9eb7c9386ba0"
},
"primary_result": "No Threat Detected"
}
"/media/Disk1/eicar.com": {
"av_info": {
"Ahnlab": {
"scan_result_i": 1,
"threat_found": "Virus/EICAR_Test_File"
},
"Avira": {
"scan_result_i": 1,
"threat_found": "Eicar-Test-Signature"
}
},
"cdr_info": null,
"coo_info": null,
"cve_info": {
"cve": []
},
"dlp_info": {
"hits": null
},
"extraction_info": {},
"file_info": {
"display_name": "eicar.com",
"file_size": 68,
"file_type": "application/octet-stream",
"file_type_description": "EICAR virus test files",
"md5": "44d88612fea8a8f36de82e1278abb02f",
"sha1": "3395856ce81f2b7382dee72602f798b642f14140",
"sha256": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
},
"primary_result": "Infected"
},
"/media/Disk1/ri.docx": {
"av_info": {
"Ahnlab": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
},
"Avira": {
"engine_result": "No Threat Detected",
"scan_result_i": 0
}
},
"cdr_info": {
"description": "Sanitized successfully.",
"details": [
{
"action": "removed",
"count": 1,
"object_name": "OLE"
},
{
"action": "sanitized",
"object_name": "XML content"
}
],
"sanitized_file_info": {
"file_size": 10713,
"sha256": "9ef0a41cc2a8489a5d6ecc6ad15e8e5f83509f1c41fa89e81669735585eb2808"
}
},
"coo_info": null,
"cve_info": {
"cve": []
},
"dlp_info": {
"hits": {
"ssn": {
"display_name": "Social Security Number",
"hits": [
{
"after": "",
"before": "test file Hook: https://webhook.site/#/dc9c7bfa-9cf7-40a9-90e9-a25e89fb6937/3315680a-35b2-4a5b-bb90-dfc550109c70/0 SSN:",
"certainty": "High",
"certainty_score": 88,
"hit": "XXXXXXX2345",
"location": "Page 1",
"severity": 0,
"tryRedact": true
}
]
}
}
},
"extraction_info": {},
"file_info": {
"display_name": "ri.docx",
"file_size": 12662,
"file_type": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
"file_type_description": "Microsoft Word Document",
"md5": "0a5af08976219fb9038c8745ca2a60b0",
"sha1": "fa15378170dd319ccb43689cc3e45aed54908386",
"sha256": "045dc650a6f2028b63a0e7102318b35ab42af335f3bdd2168342fc4f11c91897"
},
"primary_result": "No Threat Detected"
}
},
"rootkit_allowed": {
"file_paths": [
"//dev/sda//block/0/1",
"//dev/sda1//block/0/1"
]
},
"rootkit_blocked": {
"file_paths": []
},
"skipped": {
"file_paths": []
},
"start_time": "2021-10-04T21:43:28Z",
"total_result_count": 6,
"user_question_answer": [],
"uuid": "00000000-F100-4000-B100-000000500000",
"version": 2
}
