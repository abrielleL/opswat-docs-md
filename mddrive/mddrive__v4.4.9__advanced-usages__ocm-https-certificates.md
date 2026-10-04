<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/advanced-usages/ocm-https-certificates -->

# Connect OPSWAT Central Management over HTTPS

MetaDefender Drive supports secure HTTPS connections to an on-premises OPSWAT Central Management (OCM) server. To establish this connection, the OCM server must be configured with a valid TLS certificate before Drive attempts to connect.

The behavior on the Drive side depends on whether the certificate authority that issued the OCM server certificate is trusted by the operating system:

- Certificate issued by a trusted public CA — whether standalone or with a complete chain: Drive connects automatically — **no user action required**
- Self-signed certificate — whether standalone or with a private root CA chain: Drive displays an **Invalid Certificate** warning — **user must accept to proceed**

This page covers the two self-signed certificate configurations, which are the most common in isolated or air-gapped on-premises deployments.

- [Scenario 1: OCM Uses a Complete Certificate Chain with a Private Root CA](https://www.opswat.com/docs/mddrive/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain)
- [Scenario 2: OCM Uses a Standalone Self-Signed Server Certificate (No Chain)](https://www.opswat.com/docs/mddrive/advanced-usages/ocm-uses-a-server-certificate-without-a-chain--for-example--self)

After configuring OCM with a self-signed certificate (either scenario above), complete the following steps on the MetaDefender Drive side when connecting for the first time:

1. Enter the OCM server URL and registration code in MetaDefender Drive, then initiate the connection.
2. When the "Not Secure Connection" dialog appears with the message "MetaDefender Drive cannot verify the certificate presented by the Central Management server.", review the server details.
3. Click Proceed to accept the risk and add the OCM server's certificate to MetaDefender Drive's trusted certificate store.
