<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/integrations/sftp -->

# SFTP Integration

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Hosts reachable via SFTP can be integrated with MetaDefender Managed File Transfer for various use cases, such as file transfer automation. For more information, visit the [Introduction to File Transfer Automation](/docs/mdmft/v3.11.5/automated-file-transfer/automated-jobs) section.

To manage integration instances, go to "Settings" ***→*** "Integrations" **→** "SFTP."

SFTP integrations are globally shared, meaning every user with permissions to view them will see the same set of integrations.

## [Configuration](/docs/mdmft/v3.11.5/integrations/sftp#configuration)

To configure an SFTP integration, provide the following information:

- **SFTP Name**: The display name which can be anything. It will be used when selecting the integration instance.
- **SFTP Address**: The IP address or FQDN of the host.
- **SFTP Port**: The port on the host to connect to using SFTP.

## [Testing the Connection](/docs/mdmft/v3.11.5/integrations/sftp#testing-the-connection)

Users can test the connection to a configured integration. This test checks whether the configured port is accessible on the configured address.

Info

For security reasons, the "Test Connection" function only checks the address and port reachability.

Your SFTP integration with MetaDefender® MFT is now complete. Learn how to configure Automated Jobs using the same integration [here](/docs/mdmft/v3.11.5/automated-file-transfer/spo-push-files).
