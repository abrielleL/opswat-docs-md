<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-troubleshoot-https-failure-on-metadefender-core- -->

# How to troubleshoot HTTPS failure on MetaDefender Core?

This article applies to all MetaDefender V5 releases deployed on Windows or Linux systems.

You are planning on setting up HTTPS or updating HTTPS certificate.

Whenever you’re enabling HTTPS for MetaDefender Core, a number of issues can occur, the aim of this article is to outline some common issues and how to troubleshoot and resolve them.

Issue

After enabling HTTPS and restarting MD Core service, the management console is inaccessible.

When this happens, it is most likely caused by NGINX error. To troubleshoot this, you can view the NGINX’s error logs for the specific error message, located here:

- Windows: C:\Program Files\OPSWAT\MetaDefender Core\nginx\nginx_error.log
- Linux: /var/log/nginx/error.log

Error

“SSL: error:0B080074:x509 certificate routines:X509_check_ private_key:key values mismatch”

## [Possible cause:](/docs/mdcore/knowledge-base/how-to-troubleshoot-https-failure-on-metadefender-core-#possible-cause)

The HTTPS certificate and private key are mismatched. You can verify this by running the following commands:

BashCopy# Replace "cert.crt" with the path to the certificate
openssl x509 -noout -modulus -in cert.crt | openssl md5
# Replace "key.key" with the path to the private key
openssl rsa -noout -modulus -in key.key | openssl md5

If the output MD5 hash values of the certificate and private key don’t match up, then they will result in the SSL error above.

## [Remediation Steps:](/docs/mdcore/knowledge-base/how-to-troubleshoot-https-failure-on-metadefender-core-#remediation-steps)

To solve this issue, generate a new certificate-private key and ensure that they match each other.

1. If the MD Core management console is still inaccessible, use the [HTTPS Configuration Removal Tool](/docs/mdcore/troubleshooting/https-disablement-tool) and access the management console via HTTP.
2. Follow the steps to [enable HTTPS](/docs/mdcore/configuration/enabling-https) using the newly generated certificate-private key pair.

Error

"SSL__CTX__use_certificate("C:/Windows/Temp/ometascan/https_cert.pem") failed (SSL: error:0A00018E:SSL routines::ca md too weak)”

For other HTTPS failure, please follow instructions in this article [HTTPS Failure on MetaDefender Core 5.2.0 (or newer)](/docs/mdcore/troubleshooting/metadefender-core-service-failed-due-to-weak-cipher)

Support:

If you have followed the instructions above but are still encountering **HTTPS failure on MetaDefender Core**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
