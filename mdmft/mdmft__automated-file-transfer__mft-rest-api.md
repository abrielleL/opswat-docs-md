<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/mft-rest-api -->

# MFT REST API - Example

Summarize Page    Connect to Cursor Connect to VS Code
## [Secure Your Digital Ecosystem with OPSWAT MetaDefender API](/docs/mdmft/automated-file-transfer/mft-rest-api#secure-your-digital-ecosystem-with-opswat-metadefender-api)

In today’s threat landscape, proactive cybersecurity is non-negotiable. OPSWAT MetaDefender API empowers developers and security teams to seamlessly integrate advanced threat prevention into their applications and workflows. With industry-leading multi-scanning, deep content disarm and reconstruction (CDR), and vulnerability assessment capabilities, MetaDefender ensures files, devices, and data are thoroughly inspected and sanitized before they enter your environment. Whether you're building secure file upload portals, automating malware detection, or enforcing zero-trust policies, MetaDefender API delivers scalable, reliable protection that meets the demands of modern infrastructure.

💡 **Everything you can do through the MetaDefender Managed File Transfer UI, you can also do via the API**—enabling full automation and integration into your existing systems and processes.

### [**Example Use Case: Automated File Processing**](/docs/mdmft/automated-file-transfer/mft-rest-api#example-use-case-automated-file-processing)

In this scenario, a lawyer's office utilizes an automated workflow to securely handle file transfers and processing:

1. **Initial Upload** A user uploads a file to **MFT1**, located within a **low-security network**.
2. **Security Validation** Once the file is confirmed to be safe, it is automatically transferred to **MFT2** in the **high-security zone**.
3. **Automated Processing via APIs** Leverage MetaDefender MFT’s API capabilities to enhance file handling:

   - **OCR Integration (API 1):** Your application takes file from MFT1 and converts scanned documents into searchable text.
   - **Data Management:** Your application then adds relevant case information to the you database.
   - **Data Loss Prevention (API 2):** Detect and remove sensitive information, generating redacted versions of the document safeguarding against leaks of personal data.
   - **Folder Creation (API 1):** Your application then creates a case folder on MFT1 and share it with designated stakeholders.
4. **User Notification** MFT will notify all involved users once the files have been uploaded, processed, and shared, ensuring transparency and traceability throughout the workflow.

## [Quick start?](/docs/mdmft/automated-file-transfer/mft-rest-api#quick-start)

Here is mini series on how to build similar application with examples written in PoweShell. Of course you can use any other programming language you like.

- [Hello World! - Authentication and version check](./api-authentication)
- [List my files](api-list-my-files-and-folders)
- Make a folder
- Upload single file
- Upload group of files
- Create a user
- Share my file or folder
- Delete user and their files
- Triggers
