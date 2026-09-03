<!-- source: https://www.opswat.com/docs/mdmediafirewall/reports/report-schema -->

# Report Schema

Here you will find an explanation of the `JSON` report schema

### [**allowed**](/docs/mdmediafirewall/reports/report-schema#allowed)

- **file_paths**: JSON array of files with Allowed result

ExampleCopy"allowed": {
"file_paths": [
"/media/Disk2/USB/sample.txt",
"/media/Disk2/USB/figures.png",
"/media/Disk2/USB/update.exe"
]
}

---

### [blocked](/docs/mdmediafirewall/reports/report-schema#blocked)

- **file_paths**: JSON array of file paths with a Blocked result

---

### [blocked_av](/docs/mdmediafirewall/reports/report-schema#blocked_av)

- **file_paths**: JSON array of file paths with a Blocked result from the onboard AV scanning

---

### [blocked_manifest](/docs/mdmediafirewall/reports/report-schema#blocked_manifest)

- **file_paths:** JSON array of file paths with a Blocked result from the signed manifest on the media

---

### [cdr](/docs/mdmediafirewall/reports/report-schema#cdr)

- **file_paths**: JSON array of file paths that were sanitized

---

### [**client_identity**](/docs/mdmediafirewall/reports/report-schema#client_identity)

JSON object containing a collection of scan clients with their respective info:

- **clients**: array of scan clients

  - **product_type**: name of the product that performed scanning of files
  - **name**: display name of the system
  - **scan_profile**: name of the scan profile used
  - **session_id**: the ID of the scan session
  - **timestamp**: UNIX epoch timestamp of the start of the scan session
  - **av_info**: JSON object containing objects describing the scanning engines used from the product

    - key is the **name of AV engine**
    - **def_time**: timestamp of the last time the engine was updated
    - **eng_id**: string used to identify the engine

---

### [complex_archives](/docs/mdmediafirewall/reports/report-schema#complex_archives)

- **file_paths**: JSON array of file paths that are archives with identified issues

---

### [**concealed**](/docs/mdmediafirewall/reports/report-schema#concealed)

- **file_paths**: JSON array of file paths not found in the manifest

---

### [**coo**](/docs/mdmediafirewall/reports/report-schema#coo)

- **file_paths**: JSON array of file paths blocked due to Country Of Origin

---

### [dlp](/docs/mdmediafirewall/reports/report-schema#dlp)

- **file_paths**: JSON array of file paths corresponding to sensitive data found results

---

### [**encrypted**](/docs/mdmediafirewall/reports/report-schema#encrypted)

- **file_paths**: JSON array of file paths that are encrypted/password protected

---

### [**end_time**](/docs/mdmediafirewall/reports/report-schema#end_time)

scan end timestamp

---

### [**infected**](/docs/mdmediafirewall/reports/report-schema#infected)

- **file_paths**: JSON array of infected file paths

---

### [**manifest_valid**](/docs/mdmediafirewall/reports/report-schema#manifest_valid)

(optional): *boolean* value

`true` if the manifest was valid

`false` if the manifest was invalid

*missing* if the manifest could not be validated

---

### [**media_errors**](/docs/mdmediafirewall/reports/report-schema#media_errors)

- **file_paths**: JSON array of file paths that MMF had issues with validating

---

### [**media_type**](/docs/mdmediafirewall/reports/report-schema#media_type)

*string* value

Type of media scanned: `USB-A`, `USB-C`, `SD Card`, `MicroSD Card`, `Compact Flash`

---

### [**name**](/docs/mdmediafirewall/reports/report-schema#name)

name for this specific report made from internal instance ID, date, and time

---

### [**paths**](/docs/mdmediafirewall/reports/report-schema#paths)

JSON array of mount points for scanned media

---

### [**result_set**](/docs/mdmediafirewall/reports/report-schema#result_set)

JSON object containing objects for individual file results

- key is the **full path to the file**

  - **av_info**: (optional) JSON object containing onboard AV scan engine results for the file (if it was scanned)

    - **scan_result_i**: integer of the scan result
    - **scan_time**: time taken to scan (in seconds)
    - **threat_found**: name of detected threat
  - **file_info**: JSON object containing details about this file

    - **display_name**: display name for this file
    - **file_size**: size of file
    - **sha256**: SHA256 hash of file
  - **primary_result**: the overall scan result determined from all engine results
  - **transfer_info**: JSON object containing details on where the file was sent when **primary_result** is `Allowed`, *empty* for any other primary result.

    - **final_destination**: file path from the root of the `Firewall` drive available on the Host
    - **method**: `firewall` -> files are displayed on the Firewall drive
    - **success**: *boolean* (`true` or `false`)

ExampleCopy"result_set": {
"/media/Disk2/clean/tempFile1.txt": {
"file_info": {
"display_name": "tempFile1.txt",
"file_size": 10485760,
"sha256": "e5b844cc57f57094ea4585e235f36c78c1cd222262bb89d53c94dcb4d6b3e55d"
},
"primary_result": "Allowed"
},
"/media/Disk2/encrypted/passwordProtected.docx": {
"file_info": {
"display_name": "passwordProtected.docx",
"file_size": 17920,
"sha256": "db1ae075e1da0063c7f10d225fad92ab88eeb227c65957c378d7dcbfd563ed15"
},
"primary_result": "Password Protected Document"
},
"/media/Disk2/personal-data/dlp_sample.txt": {
"file_info": {
"display_name": "dlp_sample.txt",
"file_size": 132,
"sha256": "16331c34029a4bd665b02e3d3864ec104e4f76f0cb74dc58c4b2e31b6afad97c"
},
"primary_result": "Sensitive Data Found"
},
"/media/Disk2/threats/eicar.txt": {
"file_info": {
"display_name": "eicar.txt",
"file_size": 57344,
"sha256": "f8b129b4927e5419758bbdcdd167a76a96982830fa4674b939aabc5b0a3eeb8a"
},
"primary_result": "Infected"
},
"/media/Disk2/new.txt": {
"file_info": {
"display_name": "new.txt",
"file_size": 300,
"sha256": "898ef90e34acb681c3a2f102a866a71802605g1468f92a9faebfd03c7e6c75d5"
},
"primary_result": "Concealed"
}
}

---

### [**session_error**](/docs/mdmediafirewall/reports/report-schema#session_error)

(optional): *string* error message.

Message if there was an issue that stopped the session before completion

---

### [**session_type**](/docs/mdmediafirewall/reports/report-schema#session_type)

type of session

- `validation` -> Session where a media manifest was used

---

### [**start_time**](/docs/mdmediafirewall/reports/report-schema#start_time)

scan start time

---

### [**total_result_count**](/docs/mdmediafirewall/reports/report-schema#total_result_count)

total count of all files seen

---

### [vulnerable](/docs/mdmediafirewall/reports/report-schema#vulnerable)

- **file_paths**: JSON array of file paths that MMF had issues with validating

---

**uuid:** (internal use only)

**version:** (internal use only)
