<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops -->

# Why is OCM v7 failing to download engine updates even if the OPSWAT update server is whitelisted?

**Check Your Version:**

This article applies to all MetaDefender Central management v7 releases

## [**Summary**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#summary)

When OPSWAT Central Management (OCM) v7 attempts to download engine updates from
`https://update.dl.opswat.com`, the connection may fail if the customer’s network uses an **HTTPS inspection gateway** (proxy, firewall, or secure web gateway) that **re-signs TLS traffic with an internal certificate**.

In this scenario, OCM does not trust the re-signed certificate unless the **inspection gateway’s certificate chain** is imported into the **Java keystore** used by OCM.

---

## [**Symptoms**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#symptoms)

- OCM engine updates fail to download
- SSL/TLS or certificate validation errors in OCM logs
- When accessing `https://update.dl.opswat.com` in a browser from the same network, the displayed certificate:

  - Is issued by an **internal corporate CA**
  - Does **not** match OPSWAT’s public certificate chain

---

## [**Cause**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#cause)

The customer’s network is using an **SSL/TLS inspection gateway** (also known as HTTPS inspection or TLS interception).
This device:

1. Terminates the TLS connection
2. Inspects the traffic
3. Re-encrypts it using an **internal root/intermediate CA**

Java (used by OCM) does not automatically trust internal or private CAs unless they are explicitly added to its keystore.

---

## [**Resolution**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#resolution)

Import the **full certificate chain used to re-sign the traffic** into the Java keystore used by OCM.

This includes:

- Root CA certificate
- Intermediate CA certificate(s)
- The server certificate presented for `update.dl.opswat.com`(If applicable)

After importing the certificates, restart the OCM service.

---

### [**Step 1: Identify the Java Path Used by OCM**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#step-1-identify-the-java-path-used-by-ocm)

Check the OCM Java path by following the steps at <https://www.opswat.com/docs/ocm/configuration/java-configuration>

---

### [**Step 2: Check Existing Certificates in the Java Keystore**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#step-2-check-existing-certificates-in-the-java-keystore)

1. From an elevated command line interface, navigate to the Java `bin` directory, for example:

   cd "C:\Program Files\OPSWAT\Central\jreXX\bin\"
2. Run the following command to list certificates:

   keytool -list -v -keystore "C:\Program Files\OPSWAT\Central\jreXX\lib\security\cacerts" -storepass changeit

   Alternative locations (depending on Java installation):

   keytool -list -v -keystore "C:\Program Files\Java\jdkXX\lib\security\cacerts" -storepass changeitkeytool -list -v -keystore "C:\Program Files\Java\jreXX\lib\security\cacerts" -storepass changeit
3. Verify whether the following certificates are present and **not expired**:

   - The certificate presented for `update.dl.opswat.com`
   - Inspection gateway/proxy certificate
   - Intermediate CA certificate(s)
   - Root CA certificate

---

### [**Step 3: Import the Required Certificates**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#step-3-import-the-required-certificates)

If any certificates are missing, import them into the Java keystore.

Follow the official OPSWAT guide:
<https://www.opswat.com/docs/ocm/configuration/adding-certificates-to-java-keystore>

Repeat the import process for:

- Root CA
- Intermediate CA(s)
- Server certificate (if required by the gateway)

### [**Step 4: Restart OCM Services**](/docs/ocm/knowledgebase/why-is-ocm-v7-failing-to-download-engine-updates-even-if-the-ops#step-4-restart-ocm-services)

After importing the certificates:

1. Restart the **OPSWAT Central Management service**
2. Retry engine updates

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
