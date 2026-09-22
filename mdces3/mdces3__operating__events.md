<!-- source: https://www.opswat.com/docs/mdces3/operating/events -->

# Events

Summarize Page

The **Events** page provides a detailed log of **MetaDefender Cloud Email Security ™** processing history and incidents, including their severity, status, and verdict. This guide explains how to use this page effectively for monitoring and managing security events.

Search and Filtering Options

- **Search Bar**: Allows users to search for specific events based on keywords.
- **Time Range**: Narrows down events by time range.
- **Export:** The following content can be exported to CSV format (Max 10 000 entries):

  - **Event ID**
  - **Date/Time**
  - **Status**
  - **Policy**
  - **Direction**
  - **Affected Users**
  - **Verdict**
  - **Sender**
  - **Recipients**
  - **From**
  - **To**
  - **Cc**
  - **Subject**
  - **Message-ID**
  - **Size**
- **Filters:** Use the panel to narrow the list of events using one or more search criteria. It includes:

  - **Status:** Filters events by their current processing status (for example, Delivered or Quarantined).
  - **Direction:** Filters events by email direction (Inbound, Outbound, or Internal).
  - **Verdict:** Filters events by the final processing verdict.
  - **Label:** Filter events by labels attached to content.
  - **Detected By:** Filters events based on the detection engine or technology that identified the threat.
  - **Sanitized File Type:** Filters events containing sanitized files of a specific file type.
  - **Not Sanitized File Type:** Filters events containing files that were not sanitized.
  - **Sanitized Object Type:** Filters events by the type of object removed or reconstructed during sanitization (for example, Macro or Hyperlink).
  - **Message ID:** Searches for a specific email message using its unique Message ID.
  - **Subject:** Filters events by the email subject.
  - **SMTP Sender:** Filters events by the SMTP envelope sender address.
  - **From Address:** Filters events by the email sender shown in the **From** header.
  - **Recipient:** Filters events by the recipient email address.
  - **Policy Name:** Filters events processed by a specific policy.
  - **Attachment Name:** Filters events containing attachments with a specified file name.
  - **Threat Name:** Filters events by the malware or threat name reported by the detection engine.
  - **Origin Country:** Filters events based on the detected country of origin.
  - **Origin City:** Filters events based on the detected city of origin.
  - **Filter Actions:**

    - **Apply:** Applies the selected filter criteria and updates the event list.
    - **Clear:** Removes all selected filter criteria and restores the default view.
- **Column visibility:** Configure columns to display in list. Available are:

  - **Time of Event (Fixed Column):** Displays the date and time the event occurred. This column is fixed and cannot be hidden.
  - **Status:** Shows the current processing status of the event (for example, Delivered or Quarantined).
  - **From:** Displays the email sender.
  - **Affected User:** Shows the recipient or user affected by the event.
  - **Details:** Displays a summary of the event, such as the email subject or other identifying information.
  - **Policy:** Shows the policy that was applied during email processing.
  - **Verdict:** Displays the final security verdict assigned to the event.
  - **Labels:** Shows message classifications and labels, such as spam or category indicators.
  - **Direction:** Displays the email flow direction (Inbound, Outbound).
  - **Event ID:** Displays the unique identifier assigned to the event.
  - **Origin:** Displays the email origin country & city (when available)

# [Event List](/docs/mdces3/operating/events#event-list)

Each row in the event list represents an event with the following details:

- **Time of Event**: Timestamp indicating when the event occurred.
- **Event ID**: Unique identifier assigned to each security event.
- **Status**: The current status of the event:

  - **Quarantined**: Quarantined content.
  - **Delivered**: Delivered content.
  - **Investigating**: Issue under investigation.
  - **Released**: Released content.
  - **Delete**: Delete content.
  - **Closed**: Issue closed without any action.
- **Policy**: Indicates the Policy that applied for the the content.
- **Direction:** Indicates email direction (inbound/outbound).
- **Affected User**: The user impacted by the event.
- **Details**: A brief description of the email content or subject.
- **Verdict**: See [Verdicts](/docs/mdces3/configuration/verdicts).

# [Viewing Event details](/docs/mdces3/operating/events#viewing-event-details)

The **Event Overview** page provides detailed information about an individual email event, including message metadata, processing results, applied labels, associated content, and available administrative actions. It allows administrators to investigate email activity, review processed attachments, and perform actions such as releasing or deleting quarantined messages.

Depending on the event verdict and status, different actions and information may be available.

## [Event Summary](/docs/mdces3/operating/events#event-summary)

The **Event** section provides a high-level overview of how the email was processed.

It includes:

- **Time of Event:** Date and time the email was processed.
- **Processing Time:** Total time required to analyze the message.
- **Policy:** Policy applied during processing.
- **Direction:** Email flow direction (Inbound, Outbound, or Internal).
- **Verdict:** Final processing result.

Common verdicts include:

- **Sanitized**
- **Malicious**
- **Invalid File Structure**
- Other verdicts based on the applied security policy.

### [Administrative Actions](/docs/mdces3/operating/events#administrative-actions)

The available actions depend on the event status and verdict.

Possible actions include:

- **Release:** Releases a quarantined email to the intended recipient.
- **Delete:** Permanently deletes the quarantined email.
- **Release Original:** Releases the original version of a sanitized email.
- **Delete Original:** Deletes the original version while retaining the sanitized copy.
- **Actions:** Displays additional event-specific operations.

### [Labels](/docs/mdces3/operating/events#labels)

The **Labels** section displays classifications assigned during analysis.

Examples include:

- **Attachments**
- **Signed**
- **Encrypted**
- etc.

These labels provide additional context about the content.

## [Asset Details](/docs/mdces3/operating/events#asset-details)

The **Asset Details** section contains metadata about the processed email.

Information includes:

- **Item Type**
- **Affected User**
- **Origin**
- **Status**
- **Sent At**
- **Received At**
- **Quarantine ID**
- **Message ID**
- **Message Size**

- **Subject**
- **To**
- **From**
- **CC**
- **SMTP Sender**
- **SMTP Recipients**
- **Received From**
- **Last Hop IP Address**
- **Origin IP Address**

The **Status** field reflects the current state of the email, for example:

- **Delivered**
- **Quarantined**

## [Asset Actions](/docs/mdces3/operating/events#asset-actions)

Additional actions are available from the **Asset Details** section.

### [View](/docs/mdces3/operating/events#view)

The **View** menu provides access to additional message information.

#### [View Headers](/docs/mdces3/operating/events#view-headers)

Display the email headers.

#### [**View Microsoft 365 Anti-Spam Analysis**](/docs/mdces3/operating/events#view-microsoft-365-anti-spam-analysis)

Display Microsoft 365 Anti-Spam results, such as:

- SCL (Spam Confidence Level)
- BCL (Bulk Complaint Level)
- SFV (Spam Filtering Verdict)
- CAT (Category)

#### [View Quarantined Item](/docs/mdces3/operating/events#view-quarantined-item)

Redirect to the corresponding quarantined item.

### [Download Email](/docs/mdces3/operating/events#download-email)

Downloads the original email in **.eml** format for offline analysis.

This option is available only when the original email is retained.

### [Audit History](/docs/mdces3/operating/events#audit-history)

Opens the audit log for the selected event, displaying administrative actions performed on the email, such as quarantine, release, or deletion. Also allows adding custom comments.

## [Content](/docs/mdces3/operating/events#content)

The **Content** section lists every file extracted from the email, including message bodies and attachments.

Each row represents a processed object.

The table includes:

- **File Name**
- **Detection**
- **Prevention**
- **Category**
- **File Type**
- **File Size**
- **Scanned**

Use the search box to locate files by:

- File name
- File type
- File category

### [Detection](/docs/mdces3/operating/events#detection)

Displays the antivirus detection summary for each file.

Examples include:

- **0/17** – No antivirus engines detected a threat.
- **1/6** – One antivirus engine detected the file as malicious.

Selecting the detection value opens the **Event Details** page for that file.

### [Prevention](/docs/mdces3/operating/events#prevention)

Displays the Content Disarm and Reconstruction (CDR) result for each file.

Possible values include:

- **Sanitized**
- **Not Sanitized**

Selecting the prevention status opens the file's **Prevention** details.

### [Category](/docs/mdces3/operating/events#category)

Displays the detected file category.

Examples include:

- Text
- Image
- Audio or Video Format
- Document

### [File Type](/docs/mdces3/operating/events#file-type)

Displays the detected file format.

Examples include:

- ASCII Text
- Hypertext Markup Language
- Windows Media Audio
- Portable Network Graphics

### [Navigation](/docs/mdces3/operating/events#navigation)

Selecting a file from the **Content** table opens the corresponding **Content Details** page, where you can review:

- File metadata
- Antivirus engine results
- AI analysis
- Content Disarm and Reconstruction (CDR) details

This allows administrators to investigate individual files without leaving the event workflow.

# [Content Details](/docs/mdces3/operating/events#content-details)

The **Content Details** page provides comprehensive information about a scanned email attachment or file, including scan results, detection verdicts, prevention outcomes, and file metadata. It allows administrators to investigate why a file was flagged, review individual antivirus engine results, examine sanitization outcomes, and export scan information.

The page is organized into three tabs:

- **Overview** – Summary of scan and file information.
- **Detection** – Detailed antivirus and AI detection results.
- **Prevention** – Content Disarm and Reconstruction (CDR) sanitization results.

The page also includes the following actions:

- **Report Incorrect Detection:** Submit a false positive or false negative report for review.
- **Download as JSON:** Export the complete scan results in JSON format.

# [Overview](/docs/mdces3/operating/events#overview)

The **Overview** tab provides a high-level summary of the scan results together with detailed file information.

## [Scan Results](/docs/mdces3/operating/events#scan-results)

### [Advanced Threat Detection](/docs/mdces3/operating/events#advanced-threat-detection)

Displays the antivirus scan summary.

It includes:

- **Detection Count:** Number of antivirus engines that detected the file as malicious (for example, **1/6**).
- **Detection Status:** Indicates whether threats were detected.

Selecting the widget opens the **Detection** tab.

---

### [Zero-Day Malware Prevention](/docs/mdces3/operating/events#zero-day-malware-prevention)

Displays the Content Disarm and Reconstruction (CDR) result.

Possible statuses include:

- **Sanitized** – The file was successfully sanitized.
- **Not Sanitized** – The file could not be sanitized or did not meet sanitization requirements.

Selecting the widget opens the **Prevention** tab.

## [File Details](/docs/mdces3/operating/events#file-details)

Displays technical information about the scanned file.

Information includes:

- **Category:** General file category (for example, Audio or Video Format, Text).
- **File Type:** Detected file format.
- **File Extension**
- **File Size**
- **Scan Timestamp**
- **Scan Duration**
- **MD5 Hash**
- **SHA1 Hash**
- **SHA256 Hash**

These values can be used for investigation, threat hunting, or cross-referencing with external security tools.

The section also includes the following actions:

- **Add to Allowlist:** Add the file hash to the [Allowlist](/docs/mdces3/configuration/allowlist).

### [Detection](/docs/mdces3/operating/events#detection)

The **Detection** tab provides detailed results from every antivirus engine that analyzed the file.

#### [OPSWAT Predictive AI](/docs/mdces3/operating/events#opswat-predictive-ai)

Displays the verdict from OPSWAT's AI-powered malware analysis.

Possible results include:

- **No Threats Found**
- AI-generated detection verdicts when applicable

This section provides an additional layer of analysis beyond traditional antivirus engines.

#### [Advanced Threat Detection](/docs/mdces3/operating/events#advanced-threat-detection)

Summarizes the overall antivirus detection results.

It includes:

- **Detection Ratio:** Number of engines detecting the file as malicious.
- **Total Engines Scanned**

Example:

- **1/6 antivirus engines detected a threat**
- **0/14 antivirus engines detected no threats**

#### [Antivirus Engine Results](/docs/mdces3/operating/events#antivirus-engine-results)

Lists the verdict returned by each antivirus engine.

Each row displays:

- **Engine:** Antivirus engine used during scanning.
- **Verdict:** Detection result returned by the engine.
- **Definition Update:** Signature database version or update timestamp used during the scan.

### [Prevention](/docs/mdces3/operating/events#prevention)

The **Prevention** tab displays the results of Content Disarm and Reconstruction (CDR) processing.

#### [Zero-Day Malware Prevention](/docs/mdces3/operating/events#zero-day-malware-prevention)

Shows the number of objects requiring sanitization.

Possible results include:

- **Objects Sanitized** – One or more active objects were successfully removed or reconstructed.
- **No Objects Required Sanitization** – The file contained no active content requiring sanitization.

#### [Sanitization Details](/docs/mdces3/operating/events#sanitization-details)

When sanitization is performed, this table lists every object that was modified.

Information includes:

- **SHA256:** Hash of the processed object.
- **Type:** Object type (for example, Macro, Hyperlink, Embedded Object, Script).
- **Redaction:** Indicates whether the object was removed or reconstructed.
- **Sanitization Details:** Additional information describing the performed action.

Use the search field to locate a specific object by its SHA256 hash.

### [Navigation](/docs/mdces3/operating/events#navigation)

The tabs provide progressively more detailed information about the scanned file:

- **Overview** provides a summary of the scan results and file metadata.
- **Detection** displays detailed AI and antivirus engine verdicts.
- **Prevention** displays Content Disarm and Reconstruction (CDR) results and any sanitized objects.

The **Report Incorrect Detection** and **Download as JSON** actions are available from every tab, allowing administrators to report suspected false detections or export the complete event data for further analysis.
