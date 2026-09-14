<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/how-do-i-fix-issues-with-unable-to-add-https-enabled-metadefende -->

# How do I fix issues with unable to add HTTPS-enabled MetaDefender Core instance to server profile?

This article applies to MetaDefender Email Gateway Security V5 releases deployed on Windows Systems.

In some cases, when HTTPS is enabled on MetaDefender Core, you may encounter some errors when adding it to the server profiles in MetaDefender Email Gateway Security.

Cause: the HTTPS certificate of MetaDefender Core is not trusted.

Solution:

1. Check that the HTTPS certificate is issued to MetaDefender Core’s domain.

- The certificate's subject and/or ***subjectAlternativeName*** should contain the MetaDefender Core server’s FQDN or IP address.
- In the case of a wildcard certificate, it should include the MetaDefender Core server’s domain name.

2. Check that the full certificate chain, including any intermediate and root certificate authorities, is trusted on the MetaDefender Email Gateway Security server.

- You can do this by importing any intermediate and root certificate authorities to the server’s trusted root store.

3. Check that the certificate revocation list is available, reachable from the MetaDefender Email Gateway Security server, for the user account that runs the MetaDefender Email Gateway Security services.

- In the case that a certificate revocation list isn’t available, you can the following key in MetaDefender Email Gateway Security’s [registry configuration](https://www.opswat.com/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityinternal) to skip certificate revocation lists when validating certificates:

RegeditCopyParameter: ignore_certificate_revocation_list
Value: 1
Type: DWORDSupport:

In the unlikely event that you have followed the instructions above but are **Unable to HTTPS-enabled MetaDefender Core instance to server profile**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
