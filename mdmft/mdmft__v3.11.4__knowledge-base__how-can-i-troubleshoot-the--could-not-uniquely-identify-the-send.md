<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-can-i-troubleshoot-the--could-not-uniquely-identify-the-send -->

# How can I troubleshoot the 'Could not uniquely identify the sender' error when Kiosk or Email Gateway attempts to upload files to MetaDefender MFT?

Summarize Page    Connect to Cursor Connect to VS Code

A possible root cause of this issue is the presence of duplicate user accounts in MetaDefender Managed File Transfer™ with the same username. For example, there may be a third-party local user named **john.doe** and an Active Directory user with the same username also present in MetaDefender Managed File Transfer™. In such cases, deleting the third-party local user typically resolves the error.

Please note that deleting the third-party local user will move any associated files to the administrator's trash folder. Be sure to review and handle these files appropriately before proceeding with the deletion. These files cannot be restored to the corresponding user account.
