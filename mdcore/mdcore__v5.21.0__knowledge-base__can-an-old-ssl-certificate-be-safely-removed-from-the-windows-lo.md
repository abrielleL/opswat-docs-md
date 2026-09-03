<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/can-an-old-ssl-certificate-be-safely-removed-from-the-windows-lo -->

# Can an old SSL certificate be safely removed from the Windows Local Machine certificate store after updating the HTTPS certificate for MetaDefender Core?

**Check your version:**

This article applies to MetaDefender Core and is applicable to all MetaDefender Core V5 releases deployed on Windows systems.

## [**Overview**](/docs/mdcore/v5.21.0/knowledge-base/can-an-old-ssl-certificate-be-safely-removed-from-the-windows-lo#overview)

After updating the SSL certificate used for HTTPS communication by OPSWAT MetaDefender Core on a Windows platform, administrators may notice that the previous certificate is still present in the Windows certificate store. This article explains whether the old certificate can be safely removed and whether any prerequisites are required.

### [**Why the old certificate may still appear on Windows**](/docs/mdcore/v5.21.0/knowledge-base/can-an-old-ssl-certificate-be-safely-removed-from-the-windows-lo#why-the-old-certificate-may-still-appear-on-windows)

On Windows systems, updating an SSL certificate does not automatically remove the old certificate from the certificate store. MetaDefender Core updates its HTTPS configuration to reference the new certificate, but the previous certificate may remain unless it is manually deleted. Its presence alone does not indicate that it is still in use.

### [**What to verify before removing the certificate on Windows**](/docs/mdcore/v5.21.0/knowledge-base/can-an-old-ssl-certificate-be-safely-removed-from-the-windows-lo#what-to-verify-before-removing-the-certificate-on-windows)

Before deleting the old certificate from the Windows certificate store, confirm the following:

- MetaDefender Core is operating correctly over HTTPS using the new certificate
- The active HTTPS configuration in the MetaDefender Core web console under Settings > Security > Secure connection > Details displays the expected certificate
- The HTTPS configuration references the new certificate thumbprint
- The old certificate is not referenced by any active HTTPS bindings or Windows services

If these checks are satisfied, no additional preparation is required.

### [**Is it safe to delete the old certificate from Windows?**](/docs/mdcore/v5.21.0/knowledge-base/can-an-old-ssl-certificate-be-safely-removed-from-the-windows-lo#is-it-safe-to-delete-the-old-certificate-from-windows)

Yes. If the old certificate is not referenced by MetaDefender Core or any other Windows application or service, it can be safely removed directly from the Windows certificate store. No HTTPS reset, reconfiguration, or service restart is required in this scenario.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
