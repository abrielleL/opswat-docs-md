<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/country-of-origin/digital-certificate-verification -->

# Digital Certificate Verification

This feature verifies the digital signature of a file to ensure it originates from a trusted vendor. By validating the file's authenticity, it helps prevent the use of tampered or unauthorized software, enhancing overall security and trust in the file source. It is a required component for implementing an Allow List policy, where only files signed by approved vendors are permitted to bypass standard security scans.

**Configuration:** Workflow > Workflow name > Country of Origin. Enable **"Verify digital certificate"** and update the **"Trusted CAs directory"** to point to a folder that contains trusted CA files. See the **"Best Practices"** section below for instructions on how to obtain these files.

### [Verification flow](/docs/mdcore/v5.21.0/country-of-origin/digital-certificate-verification#verification-flow)

COO engine will try to look for the user’s trusted certificate inside **"Trusted CAs directory"** then try to build a trusted chain bottom up from the digital certificate used to sign the input file, up to any trusted certificate collected from "**Trusted CAs directory"**.

Only successfully verified certificates are trusted and take effect on `Action` setting. The Action setting (Block/Allow) can only be applied if the Country/Vendor filter match the certificate information and verification passed.

**Supported File Type:** Digital certificate verification in COO engine supports DLL, EXE, EXE_SFX, EFI, MSI, and CAB file types.

### [Example: Allowing Files Signed by a Specific Vendor](/docs/mdcore/v5.21.0/country-of-origin/digital-certificate-verification#example-allowing-files-signed-by-a-specific-vendor)

In this example, we will configure the system to allow all files signed by OPSWAT. Any other files will go through the regular scanning process.

#### [1. Collect Trusted CA files:](/docs/mdcore/v5.21.0/country-of-origin/digital-certificate-verification#1-collect-trusted-ca-files)

- Created a folder to store Trusted CA files, e.g.: C:\OPSWAT\TrustedCA
- Choose a file that is digitally signed by OPSWAT and that you want to allow.
- Right-click the file and select **Properties**. Go to the **Digital Signature** section, click **Details**

- In the **Signer Information** section, click **View Certificate** to open the certificate details window.

- In the **Details** tab, click on the **OPSWAT, Inc.**, then click **View Certificate** to open its details. Follow the Wizard to save the .CER file to the **C:\OPSWAT\TrustedCA** folder

**Notes**: If a customer exports a root certificate (e.g., **"DigiCert Trusted Root G4"**), the COO engine will validate the entire certificate chain — including intermediate certificates like **"DigiCert Trusted G4 Code ..."** and the leaf certificate (e.g., **"OPSWAT, Inc."**) — to ensure both integrity and trust.

#### [2. Configurations:](/docs/mdcore/v5.21.0/country-of-origin/digital-certificate-verification#2-configurations)

- In the **Action** section, select **Allow**.
- Under **Vendor Filters**, configure the rule to allow **"OPSWAT, Inc." (**can use ".*" because the trusted certificate already indicates the file from OPSWAT**).**

Info

Note: This value is taken from the Signer Name in the digital certificate.

Note:

- Enable the option **"Treat as Unknown if vendor name does not match"**. This ensures that any file failing signature validation will be scanned instead of being blocked.
- Do not select any option under **"Enable further processing with results"** to avoid unintended scans.

When processing files from OPSWAT with a valid digital signature:

- The file will match the trusted vendor filter ("OPSWAT, Inc.").
- The configured action **Allow** will be applied.
- The file will bypass the regular scanning process and be allowed without further inspection.

If the vendor information is manipulated in the file or not matched the configured vendor name, it will be processed further by other engines for full analysis.
