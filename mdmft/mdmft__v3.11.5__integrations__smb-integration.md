<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/integrations/smb-integration -->

# SMB Integration

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Hosts with SMB file shares can be integrated with MetaDefender Managed File Transfer™ for various use cases, such as file transfer automation. To learn more, visit the [Introduction to File Transfer Automation](/docs/mdmft/v3.11.5/automated-file-transfer/automated-jobs) section.

To manage SMB integration instances, go to "Settings" → "Integrations" → "SMB."

SMB integrations are globally shared, meaning every user with permissions to view them will see the same set of integrations.

Warning

SMB encryption is not enabled by default in some Windows OS.

By default, many SMB shares (e.g., newly created shares on Windows Server 2022) do not encrypt data in transit. This means traffic between MetaDefender Managed File Transfer™ and your SMB share may be sent unencrypted unless you enable SMB encryption on the share or server.

Action: Enable “Encrypt data access” on the SMB share (Share Properties → Settings) or configure server-level encryption. See “Enable SMB encryption” below.

## [Configuration](/docs/mdmft/v3.11.5/integrations/smb-integration#configuration)

To add a new SMB Integration, click the "Add SMB Integration" button.

In the pop-up modal, provide the following information:

- **SMB Name**: The display name, which can be anything. It will be used when selecting the integration instance.
- **SMB Address**: The IP address or FQDN of the host.
- **SMB Port**: The port on the host to connect using SMB protocol.
- **SMB Share Name**: The name of the file share on the host.
- **SMB Version**: Use SMB V1 for shares supporting only SMB 1.0, and SMB V2+ for newer versions (up to 3.1.1)
- **SMB Method**: The SMB file transfer method. Prefer *Direct TCP* if supported by the host.

## [Enable SMB encryption](/docs/mdmft/v3.11.5/integrations/smb-integration#enable-smb-encryption)

Info

Please follow the configuration guidelines in your SMB server’s official documentation to enable encrypted file transfers between SMB shares and clients. The exact steps may vary depending on your Windows Server version and environment, so refer to the documentation for the most accurate and supported configuration approach.

## [Testing the Connection](/docs/mdmft/v3.11.5/integrations/smb-integration#testing-the-connection)

Users can test connection to a configured SMB integration, which checks whether the configured port is accessible on the configured address.

Info

For security reasons, the "Test Connection" function only checks the address and port reachability.

Your SMB with MetaDefender® MFT is now complete. Learn how to configure Automated Jobs using the same integration [here](/docs/mdmft/v3.11.5/automated-file-transfer/smb-pull-files).
