<!-- source: https://www.opswat.com/docs/myop/knowledge-base/why-is-ocm-not-trusting-my-md-core-server-certificate-signed-by- -->

# Why is OCM not trusting my MD Core server certificate signed by an Intermediate Central Authority

**Overview**

If MetaDefender Core is using a certificate signed by an Intermediate Certificate Authority (CA), certain requirements must be met to ensure that Central Management trusts the server certificate. This article provides guidance on configuring the certificate correctly.

**Prerequisites**

- Access to the MetaDefender Core and Central management servers
- The MetaDefender Core server certificate + private key and the Intermediate CA certificate

**Requirements**

1. **Adding the Intermediate Certificate to the Windows Certificate Store**

   1. The Intermediate CA certificate must be added to the Windows Certificate Store where Central Management resides.
   2. This ensures that the Central Management system can validate the certificate chain.
2. **Alternative: Using a Concatenated Certificate**

   1. If adding the Intermediate Certificate to the Central Management machine is not an option, a concatenated certificate must be applied on the MetaDefender Core side.
   2. A concatenated certificate contains both the MetaDefender Core certificate and the Intermediate Certificate, forming a certificate chain.
   3. You can also concatenate the RootCA certificate, but most likely, this is not required.

**Concatenating Certificates on Windows**

***Method 1: Using Command Prompt***

1. Place **MDCore.crt** and **IntermediateCA.crt** in the same folder.
2. Open **Command Prompt** (Win + R, type cmd, and press **Enter**).
3. Navigate to the folder where the certificates are stored:

`cd C:\path\to\certificates`

4. Concatenate the certificates using the copy command:

`copy MDCore.crt + IntermediateCA.crt merged_certificates.crt`

***Method 2: Using PowerShell***

1. Open **PowerShell** as **Administrator**.
2. Run the following command to merge the certificates:

`Get-Content MDCore.crt, IntermediateCA.crt | Set-Content merged_certificates.crt`

***Method 3: Using Notepad***

1. Open **MDCore.crt** and **IntermediateCA.crt** in Notepad.
2. Copy the contents of both files and paste them into a new file.
3. Save the new file as **merged_certificates.crt**.

**Concatenating Certificates on Linux**

1. Navigate to the folder containing the certificates:

`cd /path/to/certificates`

2. Use the `cat c`ommand to merge them:

`cat MDCore.crt IntermediateCA.crt > merged_certificates.crt`

**Applying the Concatenated Certificate**

- Use the **merged_certificates.crt** file along with the private key corresponding to your server certificate.
- Configure this certificate in MetaDefender Core settings.
- Once configured, the Intermediate Certificate is no longer required on the Central Management machine when integrating the MetaDefender Core instance.

**Conclusion**

By following these steps, you ensure that MetaDefender Core presents a valid certificate chain, allowing Central Management to trust the server certificate.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
