<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-does-metadefender-mft-return-http-400-on-get--vault-rest-tra -->

# Why does MetaDefender MFT return HTTP 400 on GET /vault_rest/transfer?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

MetaDefender Managed File Transfer (MFT) — all supported versions

## [Issue Description](/docs/mdmft/knowledge-base/why-does-metadefender-mft-return-http-400-on-get--vault-rest-tra#issue-description)

Calling the MetaDefender MFT API endpoint `GET /vault_rest/transfer` to initiate or list transfers returns HTTP 400 with the message below when the uploader group context is not resolvable:

{
"message": "The file uploader group is required",
"ui_message_key": "UPLOAD_FILE_UPLOADER_GROUP_IS_REQUIRED",
"status_code": "BadRequest"
}
## [Cause (why this 400 error happens)](/docs/mdmft/knowledge-base/why-does-metadefender-mft-return-http-400-on-get--vault-rest-tra#cause-why-this-400-error-happens)

- API must resolve exactly one uploader-enabled group for the authenticated user.
- If zero or multiple uploader-capable groups are found, the request is rejected as ambiguous.
- Unlike the UI, the API never prompts for "Upload as group"—the group must be inferable or provided by the flow.

When the server cannot resolve a single uploader group, it returns HTTP 400 with ui_message_key UPLOAD_FILE_UPLOADER_GROUP_IS_REQUIRED.

*Example (ambiguous uploader context):*

GET /vault_rest/transfer HTTP/1.1
Host: example.mft.local
Authorization: Bearer eyJhbGciOi...
HTTP/1.1 400 Bad Request
Content-Type: application/json
{
"message": "The file uploader group is required",
"ui_message_key": "UPLOAD_FILE_UPLOADER_GROUP_IS_REQUIRED",
"status_code": "BadRequest"
}

This response is produced by request validation before any transfer object is created.

Ambiguity in the uploader context causes the 400 error; ensure the account resolves to exactly one uploader-capable group for the request.

## [Recommended Solution](/docs/mdmft/knowledge-base/why-does-metadefender-mft-return-http-400-on-get--vault-rest-tra#recommended-solution)

- Use a dedicated service account or a system-level API key for automation, and assign exactly one appropriate uploader group.
- Ensure each API user has unambiguous group membership (avoid multiple uploader-capable groups for the same account).
- Keep the initial transfer request minimal—send only `Authorization: Bearer {token}` when initiating the transfer and follow the documented sequence.
- Optionally enable the feature that lets uploads proceed without explicit group selection: [**Allow Users to Upload Files Without Specifying Group Membership**](https://www.opswat.com/docs/mdmft/configuration/file-settings#allow-users-to-upload-files-without-specifying-group-membership). Review general upload behavior here: [**Upload files (UI)**](https://www.opswat.com/docs/mdmft/operating/upload-files).

For authentication details and the end-to-end upload workflow, see:

- <https://www.opswat.com/docs/mdmft/automated-file-transfer/api-authentication>
- <https://www.opswat.com/docs/mdmft/automated-file-transfer/api-upload-a-file>
Support:

If you require further assistance, please follow the instructions on creating a support package before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
