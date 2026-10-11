<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-am-i-unable-to-enable-https-for-multiple-kiosks-or-metadefen -->

# Why am I unable to enable HTTPS for multiple Kiosks or MetaDefender Core instances managed through OPSWAT Central Management?

> **Check Your Version:** This article applies to OPSWAT Central Management SaaS version 10.3.2511+ and On-Premises version 10.3.2511+, kiosk 4.7.11+ and Core 5.16.1+

## **Issue**

HTTPS settings cannot be successfully enabled for multiple remote MetaDefender Kiosk or MetaDefender Core instances through an OPSWAT Central Management group policy following the instruction at [Certificates Management - My OPSWAT Central Management](https://www.opswat.com/docs/cm/configurations/certificates-management#assign-to-policy)

## **Possible Causes**

This issue may occur in either of the following situations:

- Each Kiosk or Core instance uses a different fully qualified domain name (FQDN), but a group policy is configured to assign the same TLS certificate to all instances in the group.
- A self-signed certificate is being used, but the certificate is not trusted by the systems or clients connecting to the Kiosk or Core instances.

When Central Management 10 applies HTTPS settings through a group policy, the same certificate is currently deployed to every Kiosk or Core instance assigned to that policy. If the certificate does not include the FQDN of each managed instance, certificate name validation may fail.

## **Resolution**

### **Use a Wildcard Certificate**

Use a wildcard certificate that covers the FQDNs of all Kiosk or Core instances in the group.

For example, if the instances use the following FQDNs:

- `kiosk1.example.com`
- `kiosk2.example.com`
- `core1.example.com`

A certificate issued for `*.example.com` can be assigned through the Central Management group policy.

Alternatively, use a certificate whose Subject Alternative Name (SAN) field includes the FQDN of every managed instance.

### **Trust the Self-Signed Certificate**

When using a self-signed certificate, import the certificate—or the root certificate that issued it—into the **Trusted Root Certification Authorities** store on all systems that need to establish a trusted HTTPS connection.

After importing the certificate, restart the affected service or browser session as necessary and verify the HTTPS connection again.

## **Recommendation**

For environments managing multiple Kiosk or Core instances through the same Central Management group policy, OPSWAT recommends using a certificate that is valid for all assigned instance hostnames, such as a wildcard or multi-domain SAN certificate.

> **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
