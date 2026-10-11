<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-do-i-fix-module-update-error----error-parsing-metadescriptor -->

# How do I fix module update error “Error parsing metadescriptor, message='Could not download metadescriptor'”?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Versions:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

### [Cause](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-fix-module-update-error----error-parsing-metadescriptor#cause)

This error occurs when there is connection issue between MetaDefender Core and the update server, such as proxy server not configured correctly, update server unreachable, or SSL issues.

### [Solution: If MetaDefender Core is updating from the Internet](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-fix-module-update-error----error-parsing-metadescriptor#solution-if-metadefender-core-is-updating-from-the-internet)

MetaDefender Core pulls engine updates from `update.dl.opswat.com` when Internet update is configured, to avoid issue:

1. Make sure that [update.dl.opswat.com is reachable from the MetaDefender Core server](/docs/mdcore/v5.22.1/knowledge-base/what-links--target-services-or-target-host-ip-s-need-to-be-allow) .
2. If a proxy is used, please make sure it’s configured correctly in [Proxy Configuration](/docs/mdcore/v5.22.1/configuration/proxy-configuration).

Certificate not available on the server's trusted certificate store

Although the **Trusted Root Certificate Authorities** store is updated frequently from Microsoft’s repository by the operating system, in some rare cases, the SSL certificate used by [update.dl.opswat.com](http://update.dl.opswat.com/) might be missing from the MetaDefender Core server’s trust store.

When the above certificate error occurs for `update.dl.opswat.com`, you might find the following in core.log:

To remediate this issue, manually access [https://update.dl.opswat.com](https://update.dl.opswat.com/) from a browser, and download the certificate chain:

View “[https://update.dl.opswat.com](https://update.dl.opswat.com/)” certificate.

Export “[https://update.dl.opswat.com](https://update.dl.opswat.com/)” certificate.

Once the certificate chain is downloaded, export the root and intermediate certificates:

Export the root and intermediate certificates.

Then, manually import each certificate in the chain (including root and intermediate certificates) into the server’s trust store:

- Windows:

  1. Double-click the .crt file → opens "Certificate".
  2. Click "Install Certificate...".
  3. Choose "Local Machine" (You will need Administrator rights).
  4. Choose "Place all certificates in the following store"
  5. Click Browse → select Trusted Root Certification Authorities.
  6. Click Next, then Finish.
- Debian:

  1. Copy your certificate to the trusted directory: `sudo cp mycert.crt /usr/local/share/ca-certificates/`
  2. Update CA store:`sudo update-ca-certificates`
- RedHat Enterprise Linux:

  1. Copy the certificate: `sudo cp mycert.crt /etc/pki/ca-trust/source/anchors/`
  2. Update CA Trust: sudo update-ca-trust extract

After that, restart “OPSWAT MetaDefender Core” service, and the certificate for `update.dl.opswat.com` should be trusted.

### [Solution: If MetaDefender Core is managed by OPSWAT Central Management](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-fix-module-update-error----error-parsing-metadescriptor#solution-if-metadefender-core-is-managed-by-opswat-central-management)

MetaDefender Core is pulling module updates from OCM, to avoid SSL issue:

1. If [OCM is using a certificate for HTTPS connection](https://www.opswat.com/docs/ocm/configuration/enabling-https), make sure that the certificate subject’s common name matches the OCM server’s URL.
2. The OCM server’s certificate must also be trusted on the MetaDefender Core server by importing to the server’s trust store.
3. The OCM server’s address must be resolvable from the MetaDefender Core server.

Support:

If you have followed the instructions above but are still unable to update MetaDefender Core modules with the error message “Error parsing metadescriptor, message='Could not download metadescriptor'”, please follow these instructions on [**How to Create Support Package With Bundle Tools?**](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
