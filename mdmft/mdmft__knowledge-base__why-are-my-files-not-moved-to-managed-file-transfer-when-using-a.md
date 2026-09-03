<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-are-my-files-not-moved-to-managed-file-transfer-when-using-a -->

# Why are my files not moved to Managed File Transfer when using Active Directory/SSO Integration?

Summarize Page    Connect to Cursor Connect to VS Code Applies to:

MetaDefender Kiosk version 4.7.6 and earlier

MetaDefender Kiosk supports transferring files to Managed File Transfer (MFT) using an associated Active Directory (AD) or SSO (Single Sign-On) account. For configuration details, please refer to:

[****Copying files to a designated locations****](https://www.opswat.com/docs/mdkiosk/operating/selecting-how-to-handle-processed-files#copying-files-to-a-designated-locations)

## [**Issue Description**](/docs/mdmft/knowledge-base/why-are-my-files-not-moved-to-managed-file-transfer-when-using-a#issue-description)

In scenarios where the Kiosk indicates a successful upload, but no files appear on the MFT side, the root cause is often an inability to uniquely identify the corresponding account in MFT. In such cases, the logs may display the following error:

HtmlCopy[3892] [INFO] [Jun 16, 17:44:22:815] SFT.cpp#512 SFT::InitializeGroupTransfer(): {EE59C843-01A4-403B-896C-2AA3D006DA3B} Failed to initialize group transfer: Http response code: 400 - Additional information:{"message":"Could not uniquely identify the sender.","ui_message_key":"API_MULTIPLE_SENDERS_MATCH","status_code":"BadRequest"}

This message indicates that MFT cannot determine a unique sender due to multiple accounts with matching identifiers.

## [**Root Cause**](/docs/mdmft/knowledge-base/why-are-my-files-not-moved-to-managed-file-transfer-when-using-a#root-cause)

The conflict typically arises when duplicate account names exist on the MFT server. For instance, if a user logs into the Kiosk via SSO (e.g., as a Third-Party User), and an AD account with a similar **Display Name** also exists in MFT, the system is unable to resolve the ambiguity. This results in a conflict that prevents the file transfer from completing.

## [**Example**](/docs/mdmft/knowledge-base/why-are-my-files-not-moved-to-managed-file-transfer-when-using-a#example)

As shown below, both an Active Directory user and a Local User have identical Display Names, leading to a conflict:

## [**Recommended Solution**](/docs/mdmft/knowledge-base/why-are-my-files-not-moved-to-managed-file-transfer-when-using-a#recommended-solution)

To resolve this issue, ensure all accounts have unique identifiers. This can be achieved by implementing a distinct naming convention for either Active Directory or SSO user accounts. Ensuring uniqueness across all account Display Names will allow MFT to correctly identify and match the sender.

Support:

If Further Assistance is required, please proceed to log a support case or chatting with our support engineer.
