<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft -->

# Integration with MetaDefender Managed File Transfer (MFT)

## [About MetaDefender Managed File Transfer](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#about-metadefender-managed-file-transfer)

MetaDefender Managed File Transfer offers a safe process for transferring files to and from secure networks as well as a way to safely store and limit access to files. With the native integration between MetaDefender Managed File Transfer and Metadefender Core, you can be sure that only files that were not detected as a threat will be accessible by your organization.

By integrating MetaDefender Managed File Transfer with MetaDefender Email Gateway Security you will be able to investigate blocked files easier, store the original version of sanitized files on a separate storage, save email storage by replacing attachments with URLs and more.

Inline images

To maintain a good end user experience MetaDefender Email Gateway Security won't upload/delete inline images when integrated with MetaDefender Managed File Transfer.

## [Example use cases](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#example-use-cases)

### ['No email attachment' policy](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#no-email-attachment-policy)

An organization's security policy may not allow files attached to emails to be received by certain users.

In such a case, Email Gateway Security can upload all regular attachments to MFT, and then remove these attachments from the email that gets delivered to the end user.

Based on the settings of the organization, either the users or the administrators can access the files that were originally attached to emails later from MFT (either directly from MFT, or via a link in the email body).

For such a use case, the appropriate rule in Email Gateway Security needs to be configured:

1. To remove attachments, and then
2. To upload removed attachments.

### [Secure attachment storage](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#secure-attachment-storage)

MetaDefender Managed File Transfer can be utilized as a transparent, secure storage for files attached to emails.

In MFT, email attachments are subject to continuous outbreak prevention (the files are scanned from time to time to prevent malware that was yet unknown at the time the attachment file was received.

For the best results, attachments are recommended to be removed from emails in this use case as well. So the first two steps of the setup are the same as in the previous use case.

For this use case the appropriate rule in Email Gateway Security needs to be configured:

1. To remove attachments, and then
2. To upload removed attachments,
3. To link the uploaded files to the email.

### [Offload scanning to MetaDefender Managed File Transfer](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#offload-scanning-to-metadefender-managed-file-transfer)

Businesses are usually reactive to email delays. Processing emails in Email Gateway Security can take several seconds, or even minutes (Deep CDR and Proactive DLP are more likely to cause delay) especially under heavy load.

To save time while receiving emails, Email Gateway Security can be configured to offload processing of attachments to MFT. This way Email Gateway Security will only process the relatively simple headers and body at the time of receiving, and can forward the email to the recipient almost instantly. Processing of the more complex attachments is done in parallel to the email delivery on the MFT.

Similarly to the previous use case, email recipients can access the attachments clicking the links in the email disclaimer.

For this use case the appropriate rule in Email Gateway Security needs to be configured (for details about the last three steps see the previous use-case):

1. To not scan attachments,
2. To remove attachments,
3. To upload removed attachments,
4. To link the uploaded files to the email.

### [Accessing false positive attachments](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#accessing-false-positive-attachments)

Having an attachment removed because of a false positive scan result can harden both the end users and the administrator's everyday life. By enabling MetaDefender Email Gateway Security to upload blocked files to MetaDefender Managed File Transfer an end-user can try to download the file from MFT later. MetaDefender Managed File Transfer can rescan files periodically so if a file becomes clean later the user will be able to download it.

You can also give a protection about false negatives. For more information please check [MetaDefender Managed File Transfer's Outbreak Prevention](https://onlinehelp.opswat.com/vault/8._Outbreak_Prevention.html).

### [Accessing original version of sanitized files](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#accessing-original-version-of-sanitized-files)

If you have sanitization enabled for emails you may would like to access the original files or have them on a separate storage. You can configure MetaDefender Email Gateway Security to upload original versions of sanitized files and add URLs for accessing them into the modified email.

### [Sending larger attachments and saving email storage](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#sending-larger-attachments-and-saving-email-storage)

MetaDefender Email Gateway Security can upload your attachments to MetaDefender Managed File Transfer while removing them from the original email and adding URLs for accessing them. This feature makes possible for end users to send/receive attachments which exceeds the email server's file limit and it can also save precious storage space on your email server.

## [Prerequisites and limitations](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#prerequisites-and-limitations)

You will need a running and accessible MetaDefender Managed File Transfer and an API token which can be used for uploading files. Please check [this](https://onlinehelp.opswat.com/vault/API_Authorization_Tokens.html) page for more information about API tokens. [Authentication requirement](https://onlinehelp.opswat.com/vault/5._Global_Settings.html) for downloading files should be turned off on MetaDefender Managed File Transfer.

No MetaDefender Managed File Transfer related action will take place for emails with blocked content if the selected action in the security rule is to block the whole email.

## [Browsing email attachments in MetaDefender Managed File Transfer](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#browsing-email-attachments-in-metadefender-managed-file-transfer)

MetaDefender Email Gateway Security will upload attachments to MetaDefender Managed File Transfer using this folder structure for easier browsing: "MetaDefender Email Gateway Security/<date>/<subject>*<<sender address>>*<<message id>>/".

For example:

- MetaDefender Email Gateway Security

  - 2018-09-28

    - Test subject_<test1@local>_<12345>

      - Attachment 1
      - Attachment 2
    - Test subject 2_<test1@local>_<No Message Id (456)>

      - Attachment 1
  - 2018-09-27

    - Test_<test1@local>_<555>

      - Attachment 1

No message ID

If an email doesn't have a message id "No Message Id (<random ID>)" will be used instead for unique identification.

Lookin up emails on MFT

Knowing an email's message ID or sender address (you can easily check it in [Operating/Email History (Email details)](/docs/mdemail/6.4.1/operating/email-history#email-details) makes it simple to look the email up using the MFT's search functionality.

## [Upload information in Processing history](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#upload-information-in-processing-history)

You can find information about attachment upload to MFT in the [Operating/Email History (Processing history)](/docs/mdemail/6.4.1/operating/email-history#processing-history) of an email. You will see if an attachment was successfully uploaded or if there was some error while uploading it.

## [Troubleshooting](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#troubleshooting)

### [Problems during upload](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#problems-during-upload)

If you are getting errors for upload please check the followings:

- MFT URL is correct:

  - You are using the correct format: *http(s)://<host>:<port>/vault_rest*
  - You are using http scheme for MFT without HTTPS and using http scheme for MFT with HTTPS
  - You are using the port for REST API and not the port for UI
- MFT API key is correct
- MFT is accessible from the machine where MetaDefender Email Gateway Security is installed
- If MFT is used with HTTPS enabled then the certificate can be trusted on the machine where MetaDefender Email Gateway Security is installed

### [Unexpected host in MetaDefender Managed File Transfer URLs](/docs/mdemail/6.4.1/integrations/integration-with-metadefender-mft#unexpected-host-in-metadefender-managed-file-transfer-urls)

URLs inserted into emails are generated by MetaDefender Managed File Transfer. If you experience URLs with unexpected host in them then you should configure MetaDefender Managed File Transfer's host which is used for accessing the UI and link generation. More information can be found [here](https://onlinehelp.opswat.com/vault/Enable_HTTPS.html).
