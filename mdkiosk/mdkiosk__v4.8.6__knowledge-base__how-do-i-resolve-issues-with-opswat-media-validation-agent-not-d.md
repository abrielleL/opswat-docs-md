<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-resolve-issues-with-opswat-media-validation-agent-not-d -->

# How do I resolve issues with OPSWAT Media Validation Agent not detecting USB after Certificate installed?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Issue**:

When the user takes the USB drive that has been wiped by the Kiosk, then they scan the now empty USB drive, then plug it into a computer with OMVA installed, the customer is getting an error that says, unable to mount the USB drive. However, within the drive there is a .OPSWAT folder with the certification.

**Solution**:

Please confirm that when adding the certificate to the Trusted Root Certificate Authorities, that Local Machine option is selected and not the Current Users for the Store Location.

**Steps to check via MMC:**

1. Open MMC in Windows
2. Click on File
3. Click on Add/Remove Snap-in
4. Click on Certificate under the Available Snap-ins
5. Click on Add
6. Check to see if the Store location is set to Current User or Local Machine

**How to retrieve OMVA logs:**

After following the above steps the OMVA still cannot mount the USB drive, please submit a case to the support team. When submitting a case, please provide OMVA logs. Please follow the steps below on how to retrieve OMVA logs:

- OMVA logs JSON formatted messages of its operation. This can be used to determine the validation ran on the system and identify any media that was blocked.
- Logging can be found in the OMVA install directory: `%PROGRAMFILES(X86)%\OPSWAT\OPSWAT OMVA\LOG\omva_logs.json`
- When extracting logs from the file, the JSON objects must be wrapped within square brackets "**[ ]"** to allow for proper parsing

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
