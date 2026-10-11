<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-handle-ssl-tls-issues-with-opswat-metadefender-core-webho -->

# How to Handle SSL/TLS Issues with OPSWAT MetaDefender Core Webhook Callback?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### Overview

This article describes how to resolve SSL/TLS certificate errors that can cause the webhook callback functionality to fail in OPSWAT MetaDefender Core version 5 on both Windows and Linux platforms.

#### Environment

OPSWAT MetaDefender Core version: 5

Supported Platforms: Windows, Linux

#### Problem Description

When the webhook callback functionality is invoked, it may fail due to SSL/TLS errors. The core.log file will contain an error similar to the following:

(core.webhook) SSL/TLS failed, issue='The issuer certificate of a locally looked up certificate could not be found, No certificates could be verified'

#### Root Cause

The webhook server’s SSL certificate chain is not trusted by the operating system. This can occur if the intermediate or root certificate authorities are not installed in the local certificate store.

#### Resolution

Windows

1. Obtain the webhook server's SSL certificate chain (root CA, intermediate CA, and server certificate).
2. Open the Microsoft Management Console (mmc.exe).
3. Add the Certificates snap-in for the local computer.
4. Navigate to Trusted Root Certification Authorities > Certificates.
5. Import the root, intermediate and server certificates into the Trusted Root Certification Authorities store.
6. Restart the OPSWAT MetaDefender Core services:

- OSPWAT MetaDefender Core

After the service restart, the Trusted root certificates will be exported to a certificate located in the MetaDefender Core installation folder Data folder (by default C:\Program Files\OPSWAT\MetaDefender Core\data)

**Linux**

By default, MetaDefender Core loads root CAs from the following locations:

- /etc/ssl/certs/
- /usr/share/ssl/
- /etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem

***Steps to import the certificates:*** __

***Debian/Ubuntu***

1. sudo cp -f <cert_file> /usr/local/share/ca-certificates/
2. sudo update-ca-certificates
3. sudo systemctl restart ometascan

***CentOS/RHEL***

1. sudo cp -f <cert_file> /etc/pki/ca-trust/source/anchors/
2. sudo update-ca-trust enable
3. sudo update-ca-trust extract
4. sudo systemctl restart ometascan

#### **Validation**

After completing the steps, trigger a webhook callback to confirm that the SSL/TLS error no longer occurs. Check the core.log for any remaining warnings or errors.
