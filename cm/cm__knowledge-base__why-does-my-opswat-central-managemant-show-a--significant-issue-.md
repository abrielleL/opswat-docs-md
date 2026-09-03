<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-does-my-opswat-central-managemant-show-a--significant-issue- -->

# Why does My Opswat Central Managemant show a "Significant Issue" with a certificate-related error?

> **Check Your Version:**
>
> This article applies to all My OPSWAT Central Management releases deployed on on-premises and Cloud.

## **Issue:**

My OPSWAT Central Management (OCM10) displays a **"Significant Issue"** with a certificate-related error `"err": "Invalid item for type: rule", "err_details": {"errors": [{"error":"Contains none-existing item","key":"allow_cert.cert","value":"manifestcert"}], "name": "Kiosk"}`.

## **Root cause:**

This error occurs due to a **case-sensitive mismatch** in certificate names used for batch signing between MetaDefender Core and OCM10.

Specifically:

- The Core's workflow (e.g., Kiosk) has the **“Generate batch signature with certificate”** option enabled.

![](https://uploads.developerhub.io/prod/97qW/j3u7iwojidsc7f5ef4wx9c1zdhurj0bqrebtwkgd10jqeak8mjedykmzw1jd0du9.png)

- The certificate name defined in MetaDefender Core (e.g., `"ManifestCert"`) does **not** match the name configured in OCM10 (e.g., `"manifestcert"`).

![](https://uploads.developerhub.io/prod/97qW/sa2zy6bloa0o890837xho4gm113spolih5y4omxr8pjfsszyfrq3po9lb70oyfgw.png)

Even though the names appear similar, certificate names are **case-sensitive**. A mismatch like this breaks the link between Core and OCM10, triggering the alert.

## **Resolution:**

To resolve the mismatch, follow these steps **in MetaDefender Core UI**:

1. **Unenroll the Affected Core**

- In **MetaDefender Core UI** > Click on **Managed**

![](https://uploads.developerhub.io/prod/97qW/sshu80s8lufruruf3lrpobyi9d4jgh22fqtozercfcna453pv9g3e0f019w11tb9.png)

- Click **Unenroll**.

2. **Temporarily Disable Batch Signing**

- Go to **Workflow Management > Workflows .**
- Select the affected workflow (e.g., **Kiosk**).
- In the **General**  tab, uncheck  **“Use certificate to generate batch signature.”**
-

![](https://uploads.developerhub.io/prod/97qW/0j8i4nusn5d4k7flzwpnbgip62h1vnlvavdwu9am55jkl9a9zgnmudqinuudi611.png)

- Save changes.

3. **Correct the Certificate Name**

- Go to **Inventory > Certificates**.
- Either rename the existing certificate to match OCM (e.g., `"manifestcert"`) or add a new certificate with the correct name.

4. **Re-enable Batch Signing**

- Return to **Workflow Management > Workflows**.
- Open the workflow.
- Re-enable **“Use certificate to generate batch signature.”**
- Select the correctly named certificate (e.g., `"manifestcert"`).

![](https://uploads.developerhub.io/prod/97qW/ibst25wto0pcdfb5anb400mahosdqpdxcuccll3bmaltfgil2wrrgozwxbwcw2ej.png)

- Save changes.

5. **Re-enroll MetaDefender Core**

- Check [this link](https://www.opswat.com/docs/cm/product-management/other-products) to see how to enroll an instance to My OPSWAT Central Management

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
