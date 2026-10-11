<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi -->

# Can I upload and retrieve files to/from MFT using RFID card login on the KIOSK?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Check your version:

This article applies to MetaDefender Kiosk 4.7.x and later on Windows.

## [**Answer**](/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi#answer)

**Upload:** Works. Files can be uploaded to MFT ("Processing with MFT" or "Post-action upload") when a user is logged in via RFID.

**Retrieve:** Does not work. A user logged in via RFID cannot browse or retrieve files from their personal MFT vault. The Kiosk blocks the request up front with the message "Passwordless user can not retrieve file from MFT server."

## [Why Upload Works but Retrieve Doesn’t](/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi#why-upload-works-but-retrieve-doesnt)

This is the key architectural difference between the two operations:

### [**Upload (works with RFID)**](/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi#upload-works-with-rfid)

When the Kiosk uploads files to MFT (either "Processing with MFT" or "Post-action upload"), it authenticates to MFT using the admin-configured server connection — an API key or service account stored in the Kiosk workflow settings. The Kiosk pushes files on behalf of the user, tagging them with the resolved username (from the RFID → AD lookup), but the HTTP authentication to MFT is system-level, not user-level. No end-user password is needed.

### [**Retrieve (fails with RFID)**](/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi#retrieve-fails-with-rfid)

When retrieving files, the Kiosk must authenticate as the specific user in order to browse that user’s personal vault. This requires calling MFT’s authentication endpoint with the user’s own username and password to obtain a session scoped to that user’s permissions and file access. Since RFID login does not produce a password, this authentication step cannot be completed, and the retrieval request cannot proceed.

## [Summary](/docs/mdkiosk/v4.8.6/knowledge-base/can-i-upload-and-retrieve-files-to-from-mft-using-rfid-card-logi#summary)

| **Operation** | **Auth to MFT** | **Credential Source** | **RFID Compatible?** |
| --- | --- | --- | --- |
| Upload (post-scan) | Admin API key / service account | Kiosk config (admin sets it) | Yes |
| Retrieve (browse user vault) | User's own credentials | User's AD password | No — no password available |

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
