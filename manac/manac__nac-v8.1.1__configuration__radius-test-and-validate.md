<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/radius-test-and-validate -->

# RADIUS Test and Validate

At this point, the wireless SSID or port is now configured and ready to test. Please connect a test device to confirm functionality.

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/radius-test-and-validate#step-by-step-guide)

## [Securing Clients](/docs/manac/nac-v8.1.1/configuration/radius-test-and-validate#securing-clients)

It is strongly recommended to configure proper server validation on the client side where possible. Proper server validation is the only effective way to prevent a potential Man-In-The-Middle attack on your network users. Alternatively, using a product such as *Secure BYOD On-boarding* can automate this process for non-technical end users.

The specific configuration will vary based on the client OS and version. When the RADIUS server is configured in *Direct Mode*, the following configuration is recommended for securing the RADIUS connection:

## [Option 1 (preferred on most clients):](/docs/manac/nac-v8.1.1/configuration/radius-test-and-validate#option-1-preferred-on-most-clients)

This option specifies only the root CA of the RADIUS server certificate.

**Option 2:**

This options specifies both the root and intermediate CAs of the RADIUS server certificate.

##
