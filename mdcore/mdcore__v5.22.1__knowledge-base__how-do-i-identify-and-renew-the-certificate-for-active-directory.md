<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-do-i-identify-and-renew-the-certificate-for-active-directory -->

# How do I identify and renew the certificate for Active Directory integration in MetaDefender Core?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Overview:** This article provides guidance on identifying the certificate configured for Active Directory integration and renewing it, whenever StartTLS or SSL encryption is being used.

**Prerequisites:**

- Access to the MetaDefender Core server.
- Access to the Active Directory domain controller.

**Steps to Configure:**

1. **Identify the certificate:** Use openssl to query the LDAPS port and see the exact certificate currently serving the connection: `openssl s_client -connect <DC_IP_OR_FQDN>:636 -showcerts`
2. **Renew the Active Directory certificate:**

   - Follow the vendor’s documentation to create a certificate request, submit it to a CA, and apply the renewed certificate. For example: Microsoft’s [Enable LDAP over SSL](https://learn.microsoft.com/en-us/troubleshoot/windows-server/active-directory/enable-ldap-over-ssl-3rd-certification-authority) (external link).
   - Once the Active Directory certificate is renewed, run the above command to confirm that the renewed certificate is serving the connection.
3. **Install the certificate:** Install the renewed certificate and/or the certificate issuer on the MetaDefender Core server, similar to [Adding a new Active Directory](https://www.opswat.com/docs/mdcore/configuration/user-directories#add-new-active-directory).

**Verify the Change:** Run the openssl command after renewing the certificate to confirm the new certificate is being used.

Support:

If Further Assistance is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
