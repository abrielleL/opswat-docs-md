<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/configuration/trusting-an-https-opswat-product -->

# Trusting an HTTPS OPSWAT product

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To ensure MetaDefender Kiosk operates correctly with another OPSWAT product configured to use HTTPS (refer to the respective product's user guide for HTTPS setup), the security certificates must be fully trusted on the MetaDefender Kiosk system.

Certificate must be valid and trusted

The security certificates need to be valid and trusted by the MetaDefender system. Otherwise, Kiosk will encounter issues when integrating with other products (in HTTPS).

If a certificate chain is in use, the Kiosk system must fully trusted the chain (root certificate, intermediate certificates and end-entity certificate)

### [Trusting self signed certificates](/docs/mdkiosk/v4.8.6/configuration/trusting-an-https-opswat-product#trusting-self-signed-certificates)

To trust self signed certificates, the public certificates from the other product must be added to the Kiosk configuration.

From Kiosk WebMC, navigate to **Configuration**, select **Advanced**, expand **Certificate Handling**

Step 1. Enable **Verify SSL Certificate**

Step 2. Click on **Add self-signed certificat**e, browse to the public certificates and upload

Step 3. Click on **Save Updates**

Once the certificates are added, they will be stored in Microsoft Certificate Store (Trusted Root Certification Authority).

Alternatively, administrators can add certificates directly to Microsoft Certificate Store (as screenshot below), but they will not appear under Kiosk WebMC.
