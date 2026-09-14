<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/why-is-the-metadefender-drive-toolkit-showing-an-error-regarding -->

# Why is the Metadefender Drive toolkit showing an error regarding SSL certificate invalid during activation process?

This article applies to the Metadefender Drive toolkit deployed in Windows systems

When activating Metadefender Drive from the Toolkit, the following message can be experienced:

This messase means that there is a communication issue between the host where Metadefender Toolkit is installed and the following addresses:

- <https://activation.dl.opswat.com/> for activation of the products.
- [uppdate.dl.opswat.com](https://uppdate.dl.opswat.com/)/ For downloading the licensed engines.

To validate that this issue is actually occurring.

From the toolkit log located in :

This is the default installation directory of Metadefender Toolkit

There will be entries like the following:

{"date":"2026-01-17T18:02:22Z","level":"error","thread":38005,"msg":"curl perform error: SSL connect error","file":"Activation.cpp","line":42},

It is required to verify the following on the host:

- If there is a proxy in place that needs to be configured to allow network traffic to these addresses.
- Is the host able to complete a TLS handshake with the <https://activation.dl.opswat.com/> address with the following:

openssl s_client -connect activation.dl.opswat.com:443

Should return the details about the SSL handshake process for further investigation.

**Support**

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support-services).
