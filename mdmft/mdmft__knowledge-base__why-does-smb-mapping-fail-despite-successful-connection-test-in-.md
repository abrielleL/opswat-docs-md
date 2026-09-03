<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in- -->

# Why does SMB Mapping Fail Despite Successful Connection Test in MetaDefender Manage File Transfer?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to MetaDefender Managed File Transfer (MFT) releases deployed on Windows systems.

## [Scenario](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#scenario)

When your **MetaDefender Managed File Transfer (MFT)** jobs involving SMB mapping were failing, even though the **SMB connection test completed successfully**, the MFT server could not access the specified SMB share path, leading to errors that indicated the share was unavailable.

**For example:**

### [Important Clarification: What the SMB Connection Test Verifies](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#important-clarification-what-the-smb-connection-test-verifies)

The **SMB connection test** only confirms that the configured port (typically TCP 445) on the target server is reachable. It does **not** validate whether:

- The provided credentials are correct
- The SMB share exists and is accessible
- The integration is properly configured to execute a job

At this point, no authentication or file system access is performed. Therefore, issues such as incorrect credentials or invalid share paths may still exist — even if the connection test reports success, as illustrated below:

*The SMB integration was configured using "NetBIOS over TCP", and the environment used SMB V2+.*
__

### [Recommendation](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#recommendation)

The most reliable way to verify the integration is to run an actual job using the correct share path and credentials. This ensures both connectivity and permissions are validated end-to-end.

For example, as shown in the screenshot below, when setting up the job, you need to provide the correct credentials and share path. Additionally, make sure that the specified user account has the appropriate permissions to access the path.

MFT cannot process jobs using the SMB share

## [Root Cause](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#root-cause)

1. The SMB method was incorrectly set to **"NetBIOS over TCP"**, which is incompatible with SMB version 2 or later. SMB V2+ requires **Direct TCP** communication.
2. The SMB share path was misconfigured, using a full folder path and trailing slashes, which resulted in the MFT server failing to locate the intended share.

## [Solution Steps](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#solution-steps)

Follow these steps to correctly configure the SMB integration for use with SMB V2+:

Before integrating with SMB storage, you should first verify the SMB version used in your environment. If the SMB share is hosted on a Windows system, you can check the active SMB version by running the following PowerShell command:

PowershellCopyGet-SmbServerConfiguration | Select EnableSMB1Protocol, EnableSMB2Protocol

### [1. Change the SMB Method when you are using SMB v2](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#1-change-the-smb-method-when-you-are-using-smb-v2)

- Navigate to the SMB integration settings in MetaDefender MFT.

Please Note:

Do not use "NetBIOS over TCP" when connecting to shares using SMB V2 or above.

### [2. Specify the Correct SMB Share Name](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#2-specify-the-correct-smb-share-name)

- Use only the share name as defined on the target file server. For example:

- The *SMB Share Name* should be:

HtmlCopyscan

- Do not include trailing slashes (e.g., `scan/` or `scan\`)

### [3. Validate SMB Share Permissions](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#3-validate-smb-share-permissions)

- Ensure the SMB share name matches exactly with the shared folder configuration on the destination server.
- Confirm that the service account used in the integration has appropriate read/write access to the share.

## [Outcome](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#outcome)

After applying the above changes, the SMB mapping issue was resolved and confirmed by the customer. Jobs using the SMB integration executed successfully without further errors.

Job starts successfully

## [Additional Notes](/docs/mdmft/knowledge-base/why-does-smb-mapping-fail-despite-successful-connection-test-in-#additional-notes)

- Always match the SMB version and method appropriately:

  - SMB 1.x → NetBIOS over TCP
  - SMB 2.x/3.x → Direct TCP
- For environments using Active Directory, ensure DNS resolution is properly configured for the file server hostname.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
