<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/custom-ca-certificates -->

# Custom CA certificates

Custom certificates can be loaded in each MDSS container by placing them in the appropriate configuration directory depending on the host OS. If the directory does not exist, an empty one is created at startup. Any number of certificates can be placed in the directory and they will be loaded into MDSS.

## Configuring custom certificates on Linux

Certificates are loaded from the following path:

```bash
/etc/mdss/ca_certificates/
```

### Notes:

- All certificates should be in .crt format
- The full SSL certificate chain should be loaded in MDSS, especially if the certificate wasn't issued by a trusted CA
- Root CAs and intermediate CAs can be loaded using the same procedure

## Configuring custom certificates on Windows

Certificates are loaded from the host certificate store. In order to add new CA certificates you'll need to do the following:

- Obtain the CA Certificate: Get the root CA certificate file (usually a .cer or .crt file) from your CA administrator.
- Open Certificate Manager:
- Press the Windows Key + R, type certlm.msc, and press Enter. (This opens the local machine certificate store)
- Import the Certificate:
- Expand the Trusted Root Certification Authorities folder.
- Right-click on Certificates.
- Select All Tasks -> Import.
- Follow the Certificate Import Wizard, browsing to the CA certificate file. Make sure to place the certificate in the Trusted Root Certification Authorities store

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
