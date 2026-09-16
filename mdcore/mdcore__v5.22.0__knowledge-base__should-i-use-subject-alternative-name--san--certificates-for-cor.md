<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/should-i-use-subject-alternative-name--san--certificates-for-cor -->

# Should I Use Subject Alternative Name (SAN) Certificates for Core and Kiosk GUIs?

This article applies to all MetaDefender product releases deployed on Windows and Linux systems.

#### [Overview](/docs/mdcore/v5.22.0/knowledge-base/should-i-use-subject-alternative-name--san--certificates-for-cor#overview)

Customers may prefer to use a Subject Alternative Name (SAN) in their SSL certificate to simplify the process of securing multiple instances of Core or Kiosk. Using a SAN certificate, customers can secure as many hostnames or IPs as they like using the same SSL certificate.

As the Common Name (CN) implementation ages out from current generation browsers, customers may also be concerned that OPSWAT will deprecate support of CN-based certificates. OPSWAT currently has no plans to deprecate Common Name certificates.

However, both the Chrome browser and Microsoft Edge deprecated support for Common Name certs in 2017, and Firefox followed suit in 2022.

#### [Recommendation](/docs/mdcore/v5.22.0/knowledge-base/should-i-use-subject-alternative-name--san--certificates-for-cor#recommendation)

For convenience and greater security, OPSWAT recommends transitioning away from Common Name-based certificates and adopting the use of Subject Alternative Names instead.

#### [Steps to Configure](/docs/mdcore/v5.22.0/knowledge-base/should-i-use-subject-alternative-name--san--certificates-for-cor#steps-to-configure)

After generating your SAN certificate and private key in X509, DER-encoded format:

- Go to the Security section of each OPSWAT product's GUI
- For MD Core that's here:

- For Kiosk, the settings are here:

- Choose the new certificate/private key pair.

#### [Verify the Change](/docs/mdcore/v5.22.0/knowledge-base/should-i-use-subject-alternative-name--san--certificates-for-cor#verify-the-change)

If Chrome or Firefox previously reported a Name Mismatch error when using a Common Name certificate, you should now notice that they allow connection without throwing that error.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
