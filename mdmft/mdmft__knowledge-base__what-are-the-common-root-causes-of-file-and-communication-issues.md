<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/what-are-the-common-root-causes-of-file-and-communication-issues -->

# What are the Common Root Causes of File and Communication Issues Between MFT Instances?

Summarize Page    Connect to Cursor Connect to VS Code
## [Use Cases Involving Network Diodes and the MetaDefender Security Gateway Verification](/docs/mdmft/knowledge-base/what-are-the-common-root-causes-of-file-and-communication-issues#use-cases-involving-network-diodes-and-the-metadefender-security-gateway-verification)

License verification

Verify that your network diodes and MetaDefender Security Gateway have active, valid licenses. These solutions may not provide clear error messages if a license is invalid or expired.

Troubleshooting: If you encounter a communication/file transfer issue while using MetaDefender Security Gateway or Optical Diode to replicate MFT streams, please follow these troubleshooting steps:

1. Verify that the integration (MFT to Kiosk, MFT to MFT) works first, without the diode.
2. Verify that there are no network configuration errors elsewhere.
3. Verify that the diode is configured correctly according to the MFT-specific configuration: <https://www.opswat.com/docs/netwall/configuration/vault-stream>

- Response delay: make sure that this is not set to a low value in the MFT stream configuration.

## [Use Cases Involving MFT to MFT Configuration](/docs/mdmft/knowledge-base/what-are-the-common-root-causes-of-file-and-communication-issues#use-cases-involving-mft-to-mft-configuration)

Issue: MFT to MFT file and folder operation transfers may fail due to connectivity or configuration issues.

Troubleshooting: To troubleshoot issues that arise with MFT to MFT configuration, please verify the following:

1. Connectivity: verify the network configuration to ensure that both MFTs can communicate effectively.
2. MFT configuration: verify the MFT to MFT integration to ensure everything is set up correctly:
3. The API key and URL of the destination MFT is valid.
4. When “Transfer only supervisor approved files” is set as the Transfer policy, ensure that Supervisor approval functionality is enabled as well.
5. When “File aggregation” is enabled, ensure that both MFTs have the same users (i.e. integrated with the same AD or have the same local users created). Otherwise, file aggregation requests will be made on behalf of the API key owner.

For more information, please visit our documentation on [MFT to MFT](/docs/mdmft/configuration/vault-to-vault).

## [Use Cases Involving MetaDefender Kiosk to MFT Configuration](/docs/mdmft/knowledge-base/what-are-the-common-root-causes-of-file-and-communication-issues#use-cases-involving-metadefender-kiosk-to-mft-configuration)

Issue: Files uploaded by Active Directory (AD) users from Kiosk do not show up in newer MFT versions.

Solution: Starting from MFT version 3.6.3, different AD groups can be assigned different MD Core workflows. As a result, when AD users upload files, they need to specify which group to upload the file to.

When uploading from Kiosk, the AD group may not be specified, causing the file upload to be rejected by MFT. As a workaround, this option should be enabled:

1. On MFT web management console, go to: Settings → Global Settings → Files
2. Enable this option: Allow Users to Upload Files Without Specifying Group Membership

Issue: Files uploaded from Kiosk to MFT do not show up on MFT’s side, and Kiosk’s logs say: “No Vault was found given id”.

Solution: This can happen if the configured MFT instance in Kiosk (Configuration → Integration) does not match the one being used in the post-action settings (Workflow → File Handling):

To fix this, simply make sure that **the correct MFT instance is selected in Kiosk’s file handling section of the workflow**, instead of leaving it blank like in the above screenshot.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
