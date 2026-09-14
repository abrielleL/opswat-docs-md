<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer -->

# How to retrieve the CRL and OCSP URLs for the Server and ICA Certificates?

### [**Purpose**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#purpose)

This document explains how to retrieve the **CRL (Certificate Revocation List)** and **OCSP (Online Certificate Status Protocol)** URLs from a server's SSL/TLS certificate and its Intermediate Certificate Authority (ICA) certificate, using a web browser. These URLs are often required for configuring firewall rules to allow outbound certificate validation.

---

### [**Steps for Chrome or Edge (similar steps for Firefox)**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#steps-for-chrome-or-edge-similar-steps-for-firefox)

#### [**1. Open the Website**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#1-open-the-website)

Go to the website in question using Chrome or Edge (e.g., [https://activation.dl.opswat.com](https://activation.dl.opswat.com/), [https://update.dl.opswat.com](https://update.dl.opswat.com/)).

#### [**2. View the Certificate**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#2-view-the-certificate)

- Click the **site information icon** in the address bar.
- Click **“Connection is secure”** or **“Certificate is valid”**.
- A **certificate window** will appear.

#### [**3. Examine the Certificate Chain**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#3-examine-the-certificate-chain)

- In the certificate window, go to the **"Details"** tab (or similar, depending on the browser).
- Select each certificate in the chain one by one (server, intermediate CA) to see the details.

#### [**4. Find CRL and OCSP URLs**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#4-find-crl-and-ocsp-urls)

For each certificate, search for the following fields::

- **CRL Distribution Points**
- **Authority Information Access**

These URLs are used by clients to check if a certificate has been revoked.

---

### [**5. Compile URLs for Firewall Whitelisting**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#5-compile-urls-for-firewall-whitelisting)

For each certificate in the chain, list all:

- CRL URLs
- OCSP URLs

**Example Whitelist Entries:**

- `http://crl.example-ca.com/example-ca.crl`
- `http://ocsp.example-ca.com`

Make sure these are accessible from inside your firewall, typically over **port 80 (HTTP)**.

---

### [**Notes**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#notes)

- These URLs are not always present; absence means revocation may not be supported.
- Most revocation services (CRL/OCSP) are still served over **HTTP**, not HTTPS.
- If OCSP stapling is enabled on the server, external OCSP queries may be reduced—but firewall whitelisting is still recommended.

---

### [**Troubleshooting**](/docs/mdcore/knowledge-base/how-to-retrieve-the-crl-and-ocsp-urls-for-the-server-and-ica-cer#troubleshooting)

- If CRL/OCSP URLs are unreachable, try accessing them directly in the browser to test connectivity.
- Use browser developer tools (F12) and Network tab to watch OCSP requests in real time, if needed.

---

Support:

If **Further Assistance** is required regarding this topic, please proceed to log a [**support case or chat with a support engineer**](https://my.opswat.com/portal/support).
