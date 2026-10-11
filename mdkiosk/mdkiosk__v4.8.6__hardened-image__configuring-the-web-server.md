<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server -->

# Configuring the Web Server

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Kiosk's Management Console relies on a REST interface which runs on HTTP by default. The following can be used to further configure the REST server to harden the system.

## [Changing the default port](/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server#changing-the-default-port)

1. From the management console navigate to the `Security` page (Administrator role is required to view this setting).

*Change default port configuration*

2. In `Port`, change the value to any port that is valid and click `Apply`

## [Setting up HTTPS](/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server#setting-up-https)

By default, communication with the Management Console is not encrypted. If HTTPS is enabled, the server can enforce secure connections between client and server on an SSL channel.

**Prerequisites**

- Kiosk version **must** be greater than or equal to **4.4.5**
- Must have a certificate on the kiosk system
- If the private key is encrypted you must create a file that contains the passphrase on the system
- Note down the file paths for the certificate, private key, and or passphrase file

## [How to create a self signed certificate (optional)](/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server#how-to-create-a-self-signed-certificate-optional)

Info

This is for testing purposes only. Self signed certificates may have limited functionality due to the nature of self signing.

Using a terminal - with passphraseCopyopenssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem

Then create your passphrase file and enter your passphrase into it.

---

Using a terminal - without passphraseCopyopenssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -nodes

---

## [Adding a certificate](/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server#adding-a-certificate)

1. After completing the prerequisites you should have a certificate and private key on the system
2. From the management console navigate to the `Security` > `Certificate`page
3. Click Add new certificate
4. Fill the required input fields and click `Add`

*Add Certificate on the KIOSK WebMC*

Info

Kiosk will validate these fields and display an error at the top of the screen if an issue is detected

The page will display the successfully added certificate, which can be modified or removed, except for the one currently in use.

*Manage the added certificates*

## [Enabling HTTPS](/docs/mdkiosk/v4.8.6/hardened-image/configuring-the-web-server#enabling-https)

*Enable HTTPS*

1. From the management console navigate to the `Security` page
2. Click the `Enable HTTPS` checkbox
3. Select the preferred certificate
4. Choose the preferred TLS settings (if no options are selected then Kiosk will fall back to default TLS settings)
5. Click `Apply`
6. The Kiosk will restart its internal components and apply the changes selected

Info

This process may take approximately one minute to complete

7. Once the Kiosk services have restarted, a new tab should open that directs to the Kiosk page. If the tab does not automatically open, then click the hyperlink on the results page to open the new tab.
