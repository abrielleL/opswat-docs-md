<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-do-i-troubleshoot-https-issues-for-metadefender-managed-file -->

# How do I troubleshoot HTTPS issues for MetaDefender Managed File Transfer?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer (MFT) releases.

When configuring HTTPS for MFT or integrating with other MetaDefender products (such as Core and Kiosk) via HTTPS, you may encounter some issues if there are misconfigurations. Please follow this troubleshooting guide to remediate these issues.

Error

MetaDefender Managed File Transfer becomes unreachable after enabling HTTPS.

**Solution**: Follow the troubleshooting steps outlined in this article: [How to troubleshoot MetaDefender Managed File Transfer becomes unreachable after enabling HTTPS?](/docs/mdmft/v3.11.4/knowledge-base/how-to-troubleshoot-metadefender-managed-file-transfer-becomes-u)

Error

Unable to add HTTPS-enabled MetaDefender Core instance to MFT’s integration.

**Troubleshoot**: First, open MFT logs to determine if there are any relevant error messages to narrow down the potential causes. Please refer to [How do I find all the MFT logs and their functionality?](/docs/mdmft/v3.11.4/knowledge-base/how-do-i-find-all-the-mft-logs-and-its-functionality-) for more info on these logs.

This is most likely caused by the MD Core server’s certificate not trusted by MFT server, other certificate verification errors, or using the wrong port for MD Core. To resolve this, follow these steps:

1. Ensure MD Core’s HTTPS ports are open and reachable: 443, 8008.
2. Check that the HTTPS certificate is issued to MetaDefender Core’s domain.

   - The certificate's subject and/or **subjectAlternativeName** should contain the MetaDefender Core server’s FQDN or IP address.
   - In the case of a wildcard certificate, it should include the MetaDefender Core server’s domain name.
3. Check that the full certificate chain, including any intermediate and root certificate authorities, is trusted on the MFT server.

   - You can do this by importing any intermediate and root certificate authorities to the server’s trusted root store.
4. Check that the certificate revocation list is available, reachable from the MFT server, for the user account that runs the MFT services.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
