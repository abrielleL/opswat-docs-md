<!-- source: https://www.opswat.com/docs/filescan/adminguide/scan-url-UIofw -->

# Scan URL on the UI

### Step 1- Go to [filescan.io/scan](https://www.filescan.io/scan) page

*(replace the domain with your local/cloud version)*

Paste the target URL address to the text field and click the "**Analyze Link**" button.

### [Step 2 - Customize analysis options and accept the Term of Use and Privacy Policy](/docs/filescan/adminguide/scan-url-UIofw#step-2---customize-analysis-options-and-accept-the-term-of-use-and-privacy-policy)

#### [Basic Options](/docs/filescan/adminguide/scan-url-UIofw#basic-options)

**Tags:** You can add some description with #tags

**Optional** You can apply some optional settings:

- ***Password***: You could provide a password for password-protected archives. The following common password will be applied automatically if archive uses common password:

  - “infected”
  - “malware”
  - “virus”
  - “password”
- ***Do not share file***: This setting prohibits other community members from accessing the file. However, the reports remain public (Including screenshots and extracted texts.)
- ***Skip whitelisted***: If the file is detected as "whitelisted", the file won't be scanned and report won't be created.

#### [Advanced Options](/docs/filescan/adminguide/scan-url-UIofw#advanced-options)

Optional Authentication required For advanced options you must be authenticated. Advanced options are:

- ***Pre-configured analysis options***: It excludes the apply_fine-tune_analysis use case. If you apply this setting, then the system will apply a preconfigured profile to execute the scan. -
- ***Fine-tune key aspects of your analysis***: You can choose from the following list. The selection is optional. It is not required to select at least one.

  - **YARA (Basic)** - *Enabling YARA rule matches on input file*
  - **YARA (All)** - *Enabling YARA rule matches on extracted artefacts*
  - **File visualization** - *Enabling file visualization (e.g. PDF rendering)*
  - **Images OCR** - *Enabling OCR text recognition on extracted images*
  - **File downloads** - *Enabling downloading files from extracted URLs*
  - **OSINT Lookups** - *Enable OSINT Lookups globally*
  - **OSINT Lookups (Basic)** *- Enable OSINT Lookups on the IOCs related to the input file*
  - **OSINT Lookups (All)** *- Enable OSINT Lookups also on the extracted artifacts*
  - **Domain resolving** *- Enable Resolving domains to the IPs (DNS)*
  - **WHOIS** - *Enable WHOIS record lookups*
  - **IP geolocation** *- Enable metadata lookups for Extracted IDs*
- ***Personalization:*** You can apply this feature to save the selected configuration.

  - **Save preset**

### [Step 3 - Accept the Term of Use and Privacy Policy](/docs/filescan/adminguide/scan-url-UIofw#step-3---accept-the-term-of-use-and-privacy-policy)

Required For scan it is necessary to accept the Term of Use and Privacy Policy.

### [Step 4 - Get the report](/docs/filescan/adminguide/scan-url-UIofw#step-4---get-the-report)

After clicking the Upload button, the scanning starts. The report will appear after the scanning is finished.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
