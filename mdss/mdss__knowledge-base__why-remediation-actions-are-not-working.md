<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-remediation-actions-are-not-working -->

# Why remediation actions are not working?

This article applies to all MetaDefender Storage Security versions.

Remediation actions are executed after a successful file scan.

Please follow the steps below to analyze why remediation actions may not be working in your environment:

**Step 1: Review correct setup**

1. Make sure that the [workflow](/docs/mdss/configuration/workflows) has been setup correctly.
2. Ensure that MetaDefender Storage Security is connected to correct storage unit and there are not permission issues.
3. Check if MetaDefender Storage Security is connected to the expected [MetaDefender Core Instance](/docs/mdss/operations/workflows).

**Step 2: Ensure that there are no issue scanning files**

Remediation actions are executed after a successful file scan. If a file was not scanned, please check on MetaDefender Core the reasons why. You can review the different scan results codes in [here](https://www.opswat.com/docs/mdcore/integration/description-of-scan-result-codes).

**Step 3: Transfer Speeds**

Issues related to transfer speeds can cause file upload to take longer than expected which can cause issues performing remediation actions. For example in AWS S3 integration:

**AWS**

1. Low transfer speeds With big files, usually, there may be an extended period of time that it is used for file uploads. This can be caused due to a network infrastructure limitation. For checking the transfer speed in AWS for example, we recommend using “Server Access logging”.

2. Temporary credentials expire during file upload Depending on the transfer speeds, the temporary credentials provided by the IAM may expire mid-upload. This issue would be improved if transfer speeds improve. Alternatively, you can increase the temporary credential timeout period through AWS AIM Console settings as needed.

**Step 4: Credentials and permission to access Storage units**

Credentials and permissions are what allow access to MetaDefender Storage Security access storage units to apply remediation actions. In cases where these are not set correctly or lack enough priviledge, this function would run into issues. For example in SMB integrations:

**SMB**

1. **Permission restrictions preventing access to the SMB share.** To troubleshoot, please:

   1. Verify that the user account has appropriate permissions on the SMB share.
   2. Check both share-level and NTFS permissions for read/write access.
   3. Ensure the user account is not locked or disabled.
2. **Authentication protocol error.** This issue could result from an authentication protocol mismatch between MDSS client and your SMB server. To troubleshoot:

   1. **If your SMB server runs on Windows**: Configure the username from MDSS UI to be in UPN format ([user@domain.com](mailto:user@domain.com)) to enable Kerberos authentication
   2. **If your SMB server runs on Linux**: Use the format DOMAIN\username for NTLM authentication

Info:

Based on our analysis and extensive experience with similar connectivity challenges, we strongly recommend implementing **SMB Share via NFS Storage Unit Configuration**. This approach has consistently delivered superior results for customers experiencing SMB connectivity issues.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
