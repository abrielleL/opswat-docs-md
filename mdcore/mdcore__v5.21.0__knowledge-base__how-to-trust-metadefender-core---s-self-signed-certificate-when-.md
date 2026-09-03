<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-trust-metadefender-core---s-self-signed-certificate-when- -->

# How to Trust MetaDefender Core’s Self-Signed Certificate When HTTPS Is Enabled?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

When enabling HTTPS for MetaDefender Core, most of the times a self-signed Security Certificate is being used. In these scenarios, other products integrated directly with it, in a 1-to-1 connection (without any intermediary proxy and/or network appliance), will fail to connect due to an SSL Trust Relation not establishing anymore. To address this, the Security Certificate needs to be installed in the Trusted Root Certification Authorities store of the machine hosting the application integrated with Core. Please find below the steps to achieve this for each Operating System:

## [Windows:](/docs/mdcore/v5.21.0/knowledge-base/how-to-trust-metadefender-core---s-self-signed-certificate-when-#windows)

1. Double-click the .crt file → opens "Certificate".
2. Click "Install Certificate...".
3. Choose "Local Machine" ( You will need Administrator rights ).
4. Choose "Place all certificates in the following store"
5. Click Browse → select Trusted Root Certification Authorities.
6. Click Next, then Finish.

## [Debian:](/docs/mdcore/v5.21.0/knowledge-base/how-to-trust-metadefender-core---s-self-signed-certificate-when-#debian)

1. Copy your certificate to the trusted directory:

`sudo cp mycert.crt /usr/local/share/ca-certificates/`

2. Update CA store:

`sudo update-ca-certificates`

## [RedHat Enterprise Linux:](/docs/mdcore/v5.21.0/knowledge-base/how-to-trust-metadefender-core---s-self-signed-certificate-when-#redhat-enterprise-linux)

1. Copy the certificate:

`sudo cp mycert.crt /etc/pki/ca-trust/source/anchors/`

2. Update CA Trust:

`sudo update-ca-trust extract`

*The application service/machine needs to be restarted for the changes to take place and the SSL Trust Relation to establish.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
