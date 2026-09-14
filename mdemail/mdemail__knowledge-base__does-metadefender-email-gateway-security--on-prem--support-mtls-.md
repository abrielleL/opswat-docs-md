<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/does-metadefender-email-gateway-security--on-prem--support-mtls- -->

# Does MetaDefender Email Gateway Security (on-prem) support mTLS for SMTP connections?

This article applies to all MetaDefender Email Gateway Security instances deployed on Windows operating systems (on-premise).

**OPSWAT Email Gateway Security (EGS) On-Prem** supports **mutual TLS (mTLS)** for **outbound SMTP connections**. This allows the EGS server to authenticate with a remote SMTP server using a **client certificate** during the TLS handshake.

First, the certificate needs to be added under **Settings > Certificates**:

Then this certificate can be used for the outbound SMTP connection under **Settings > Server profiles**:

However, **mTLS is not supported for inbound SMTP connections**. The inbound SMTP server in EGS does not perform **client certificate verification**, so mutual TLS cannot be enforced for incoming SMTP sessions.

Support:

If you have any questions, concerns or issues regarding MetaDefender NetWall products, please open a [**Support Case**](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s/).
