<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/information-regarding-certificates -->

# Information Regarding Certificates

Summarize Page    Connect to Cursor Connect to VS Code
## [Using a Certificate Signed by a Certificate Authority](/docs/mdmft/v3.11.4/configuration/information-regarding-certificates#using-a-certificate-signed-by-a-certificate-authority)

Follow the CA instructions to install your certificate on your server.

Once a valid certificate is installed, export it in PKCS12 format and convert it to PEM format using a tool like "openssl."

## [Instructions for Exporting an Existing Certificate](/docs/mdmft/v3.11.4/configuration/information-regarding-certificates#instructions-for-exporting-an-existing-certificate)

1. Open "mmc" in "Windows Run."

2. Select "File" → "Add or Remove Snap-ins."

3. Add certificates → choose "Computer Account" → click "Next" → click "Finish" → click "OK."
4. Navigate to the folder where the certificate is installed.

5. Right click the certificate and select "All Tasks" → "Export" to launch the "Certificate Export Wizard."
6. Choose to export the private key with the certificate.

7. Save the certificate and private key in the PKCS12 (.PFX) format.

8. Protect the private key to a security principal or by using a password.

9. Enter a certificate name then click "Next" and "Finish."

## [Converting a PKCS12 Certificate to PEM](/docs/mdmft/v3.11.4/configuration/information-regarding-certificates#converting-a-pkcs12-certificate-to-pem)

1. (Optional) Install the openssl command line utility.
2. Open a command prompt and type the following command, replacing the certificate names and password:

openssl pkcs12 -in testcert.pfx -out testcert.pem
Enter Import Password:
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:Info

Import Password is the password used to encrypt the PKCS12 private key. The PEM passphrase is the password used to encrypt the key in PEM format.

Save it as plain text for configuring TLS/SSL. If no passphrase was used then the "-nodes" argument must also be passed.

`openssl pkcs12 -in testcert.pfx -out testcert.pem -nodes`

`Enter Import Password:`

## [Generating a Self-Signed Certificate with openssl](/docs/mdmft/v3.11.4/configuration/information-regarding-certificates#generating-a-self-signed-certificate-with-openssl)

1. Open a command prompt and type the following command, replacing the inputs with valid local paths:

openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
Generating a RSA private key
......................................................................................................++++
.........................................................................................................................................++++
writing new private key to 'key.pem'
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:
State or Province Name (full name) []:
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:

Note: The entries starting from "Country Name" may be ignored.
