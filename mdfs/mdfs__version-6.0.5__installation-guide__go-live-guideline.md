<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline -->

# Go-Live Guideline

This document serves as a comprehensive configuration guide for setting up Cloud Security for Salesforce after the package has been installed. It is intended for Salesforce administrators and MetaDefender admins responsible for enabling threat detection, file sanitization, and secure handling of user data.

Key configuration areas covered include:

- **Administration Setup** – Instructions for adding the API key, assigning required permission sets (CSFS Admin Access, Approver), and managing user access either manually or automatically.
- **File Sanitization** – Guidelines for authorizing AWS S3 endpoints in Remote Site Settings, tailored to your Salesforce organization’s server region (e.g., EU).
- **Email Scanning** – Steps for configuring Email-to-Case and routing addresses to enable email scanning.
- **Large File Support** – Notes on configuration considerations for handling large file uploads.

This guide ensures your Salesforce environment is properly secured and integrated with available features for advanced malware prevention and data sanitization.

### [Administration](/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline#administration)

- Add **API Key** into **Account Settings** section.

As a System Administrator, assign the **CSFS Admin Access** permission set to users who require access to the MDFS configuration.

- As CSFS Admin go to App Launcher → OPSWAT → OPSWAT Settings → Grant access as **CSFS Admin** to other Available users for whom is required.

As System Administrator, assign the **Approver** permission set to MDFS Admins who require approval for releasing blocked files.

- As CSFS Admin go to App Launcher → OPSWAT → OPSWAT Settings → Grant access as **Approver** to the Available CSFS Admins for whom is required.

Add User Permission Assignment:

- Manually

  - Setup → Users → [select the user] → Permission Set Assignments → Edit Assignments → add **MetaDefender User Access** in Enabled Permission Sets → Save

Automatically

- Using configuration in **User Permission Assignment Settings** section.

### [File Sanitization](/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline#file-sanitization)

- Based on your Salesforce organization server region, authorize AWS s3 endpoint in Remote Site Settings.

  - e.g. of an EU Salesforce organization server region:

    - Setup → Remote Site Settings → New Remote Site:

      - Remote Site Name: `Sanitized_Files_Host`
      - Remote Site URL: `https://s3.eu-central-1.amazonaws.com`

### [Scan Emails](/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline#scan-emails)

Setup → Email-to-Case → Edit and check the followings:

- Enable Email-to-Case
- Enable on-demand service

  - Over email rate limit action: Bounce message
  - Unauthorized sender action: Discard message

Set up Email-to-Case and define a Routing Address, using its associated Email Service Address to scan incoming emails.

### [Large File support](/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline#large-file-support)

<https://www.opswat.com/docs/csfs/file-security--metadefender-/file-security---large-file-support>

### [Testing Go-Live](/docs/mdfs/version-6.0.5/installation-guide/go-live-guideline#testing-go-live)

- Enable **Multiscan** and **Save** the configuration.

- Go to App Launcher and search for Files.
- In Files upload a file through Upload Files button.

Once the file is done uploading, go to **OPSWAT - MetaDefender Logs** and check the status of the log generated for the uploaded file. If the status of the log is **Failed to scan** something was not correctly configured during the guideline steps or you don’t have a valid API Key.
