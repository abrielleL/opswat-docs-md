<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/unable-to-connect-to-opswat-product-instances-that-have-enabled- -->

# Unable to connect to OPSWAT Product instances that have enabled HTTPS mode

| Term | Detail |
| --- | --- |
| Problem | OPSWAT Central Management cannot connect to OPSWAT Product instances that have enabled HTTPS mode. |
| Cause | The certificates for the domains that the OPSWAT Product instances belong to have not been added to OPSWAT Central Management's trust store. The product instance's server address does not match its SSL certificate |
| Troubleshooting | Testing connection returns the error "The server's security certificate is not trusted." Testing connection returns the error "Could not reach the server." |
| Solution | Ensure that the domains are trusted hosts for OPSWAT Central Management. Ensure that the product instance's server address match its SSL certificate. |

When adding a new OPSWAT Product instance that has enabled HTTPS mode, it is possible to encounter several common errors as shown below.

#### [The server's security certificate is not trusted.](/docs/ocm/7.39.0/troubleshooting/unable-to-connect-to-opswat-product-instances-that-have-enabled-#the-servers-security-certificate-is-not-trusted)

One possible cause is that the domain that the instance belong to is not recognized as a trusted host, such as because of missing certificates. Please follow the instructions at [Adding certificates to Java keystore](/docs/ocm/7.39.0/configuration/adding-certificates-to-java-keystore).

Another cause is that the certificates may be invalid if they have already been added. In this case, please verify that the certificates are valid and add them again if necessary.

#### [Could not reach the server.](/docs/ocm/7.39.0/troubleshooting/unable-to-connect-to-opswat-product-instances-that-have-enabled-#could-not-reach-the-server)

The "Could not reach the server" error is a catch-all for miscellaneous connection errors. One such error is that the product instance's server address does not match its SSL certificate

To troubleshoot this error, first locate the gears_product_service.log.

- On Windows: <Install folder>\OPSWAT\Central\tomcat\logs\gears_product_service.log
- On Linux: /opt/ocm/tomcat/logs/gears_product_service.log

As an example, we have the instance **testCore** with the server address [**https://testhost:8008**](https://testhost:8008). This instance uses the SSL certificate with the Common Name (CN) **testcore**. There should be logs of the failed connection attempt similar to the snippet below:

ProductServiceImpl - ----- Start checking connection of: testCore
ProductServiceImpl - Try to get product version
ProductServiceImpl - Exception occurs when trying to connect to instance. Root cause: HTTPS hostname wrong: should be <testhost> executing GET https://testhost:8008/version
ProductServiceImpl - Could not get product version, return message: Could not reach the server.
ProductServiceImpl - ----- Finish checking connection of: testCore
ProductServiceImpl - Could not reach the server.

The root cause "HTTPS hostname wrong: should be <testhost> executing GET [https://testhost:8008/version"](https://testhost:8008/version%22) is logged because the SSL certificate's CN **testcore** does not match with the server address [**https://testhost:8008**](https://testhost:8008)

There are several solutions for this issue:

- Change the server address to match the SSL certificate, assuming the new address is valid.

  - Using the example, you would change the server address to [**https://testcore:8008**](https://testcore:8008) to match the SSL certificate.
- Generate a new SSL certificate matching the desired server address and add it to the product instance.

  - Using the example, you would generate a new certificate with the CN **testhost** to match the desired address [**https://testhost:8008**](https://testhost:8008)**.**
