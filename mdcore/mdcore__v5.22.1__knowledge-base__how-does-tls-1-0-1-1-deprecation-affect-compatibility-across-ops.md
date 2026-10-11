<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-does-tls-1-0-1-1-deprecation-affect-compatibility-across-ops -->

# How Does TLS 1.0/1.1 Deprecation Affect Compatibility Across OPSWAT Products?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Email Gateway Security (EGS), MetaDefender Core (MD Core), MetaDefender Sandbox, MetaDefender MFT deployed on both Windows and Linux systems

**Issue**

A customer experienced issues sending emails to a specific recipient using MetaDefender Email Gateway Security (EGS) version 5.7.4. While receiving emails worked without issue, outgoing messages to this customer consistently failed. The recipient organization confirmed that their infrastructure only supports **TLS 1.1**, which is incompatible with OPSWAT’s updated TLS policies.

The customer requested guidance on enabling TLS 1.1 on various OPSWAT products (EGS, MDCORE, Sandbox) or implementing exceptions for specific IP addresses or DNS names to restore mail flow to the affected domain.

**Root Cause**

As of version **5.7.0 and later**, OPSWAT has **fully deprecated support for TLS 1.0 and TLS 1.1** across its product line. This deprecation aligns with modern security standards and is intended to protect the integrity and confidentiality of communications handled by OPSWAT products.

**Affected Products and TLS Support**

**Configuration Exceptions**

**EGS**

**No exceptions** can be made within **EGS** for specific IP addresses or domains to enable TLS 1.0/1.1. This restriction is a security safeguard designed to enforce consistent secure communication across all environments.

**MD Core**

While MD Core may technically allow for legacy protocol configuration changes (via ssl.conf.mdcore), **OPSWAT does not support or recommend** enabling deprecated TLS versions due to known vulnerabilities and risk factors.

SSL customizations are easy to manage in MD Core v14+. We recommend using the new Secure Connection Settings shown below instead of the conf file. For best security please stick with a **minimum** of TLSv1.2.

**Recommendation**

If a partner or customer is unable to upgrade from TLS 1.1 due to legacy system limitations, the following alternatives are recommended:

1. E**ngage the partner organization** to encourage the adoption of TLS 1.2 or newer protocols.
2. **Implement an SMTP relay or intermediate mail gateway** that can downgrade/upgrade TLS between the OPSWAT environment and the legacy system (acting as a secure bridge).
3. **Separate the affected communication route** from OPSWAT-secured email flow if compliance/security policies allow for temporary workarounds.

Since **v5.14.0**, MetaDefender Core supports configurable TLS versions via the **web console**. Only **TLS 1.2 and 1.3** are available. We recommend configuring TLS settings through the web console instead of the config file to reduce errors and ensure better manageability.

**Conclusion**

OPSWAT prioritizes strong encryption and secure communication protocols. TLS 1.0 and 1.1 are no longer supported, and exceptions to this rule are not possible within most OPSWAT products, including Email Gateway Security.

Customers needing assistance in architecting alternative solutions or facing similar compatibility concerns are encouraged to reach out to OPSWAT Support for tailored guidance.

**Related Documentation:**

- [OPSWAT SSL Configuration Guide](/configuration/ssl-configurations)
- [MetaDefender Email Gateway Release Notes](https://www.opswat.com/docs/mdemail/release-notes)

Support:

If Further Assistance is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
