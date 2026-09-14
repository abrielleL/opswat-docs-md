<!-- source: https://www.opswat.com/docs/ocm/configuration/adding-certificates-to-java-keystore -->

# Adding certificates to Java keystore

In certain circumstances, such as adding a product instance or an Active Directory server that have been configured to use HTTPS protocol with self-signed certificates, you may need to import said certificates to OPSWAT Central Management's Java keystore to establish a trusted connection.

Please follow the instructions below to add the certificate to the Java keystore.

Info

From version 7.23.0 on Windows, OPSWAT Central Management is integrated with Windows's Local Machine Certificate Store. Certificates that exist in Windows's Local Machine Certificate Store do not need to be imported to the Java keystore.

1. Locate the root certificate file (.crt) for the product instance.
2. From an elevated command-line interface, enter the command:

WindowsLinuxCopy"<Java installation folder>\bin\keytool" -importcert -keystore "<OCM installation folder>\jre11\lib\security\cacerts" -storepass <password> -alias "<alias>" -file "<rootCA.crt path>"
Example:
"C:\Program Files\OPSWAT\Central\jre11\bin\keytool" -importcert -keystore "C:\Program Files\OPSWAT\Central\jre11\lib\security\cacerts" -storepass changeit -alias "ocmCA" -file "C:\Users\admin\Downloads\ocm.crt""/opt/ocm/jre11/keytool" -importcert -keystore "/opt/ocm/jre11/lib/security/cacerts" -storepass <password> -alias "<alias>" -file "<rootCA.crt path>"
Example:
"/opt/ocm/jre11/bin/keytool" -importcert -keystore "/opt/ocm/jre11/lib/security/cacerts" -storepass changeit -alias "ocmCA" -file "/etc/somewhere/ocm.crt"

**<Java installation folder>:** The installation path of the Java distribution. By default, from version 7.22.0, OPSWAT Central Management uses it own bundled Java 11 distribution, located at **<System Drive>:\Program Files\OPSWAT\Central\jre11.**

**<password>:** The keystore's password.

**<alias>**: The certificate's alias.

**<rootCA.crt path>**: The path to the product instance's root certificate file.

3. Restart OPSWAT Central Management for the changes to take effect.

Info

If OPSWAT Central Management was upgraded from a version older than 7.22.0, it is most likely using a user-specified Java 11 distribution. Please refer to [Java Configuration](/docs/ocm/configuration/java-configuration) to locate the Java installation being used.
