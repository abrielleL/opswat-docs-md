<!-- source: https://www.opswat.com/docs/myop/knowledge-base/why-does-my-opswat-central-managemant-v8-show-a--significant-iss -->

# Why does My Opswat Central Managemant v8 show a "Significant Issue" with a certificate-related error?

This article applies to all My OPSWAT Central Management **v8** releases deployed on on-premises and Cloud.

## [**Issue:**](/docs/myop/knowledge-base/why-does-my-opswat-central-managemant-v8-show-a--significant-iss#issue)

OPSWAT Central Management v8 (OCM8) displays a **"Significant Issue"** with a certificate-related error `"err": "Invalid item for type: rule", "err_details": {"errors": [{"error":"Contains none-existing item","key":"allow_cert.cert","value":"manifestcert"}], "name": "Kiosk"}`.

## [**Root cause:**](/docs/myop/knowledge-base/why-does-my-opswat-central-managemant-v8-show-a--significant-iss#root-cause)

This error occurs due to a **case-sensitive mismatch** in certificate names used for batch signing between MetaDefender Core and OCM8.

Specifically:

- The Core's workflow (e.g., Kiosk) has the **“Generate batch signature with certificate”** option enabled.

- The certificate name defined in MetaDefender Core (e.g., `"ManifestCert"`) does **not** match the name configured in OCM8 (e.g., `"manifestcert"`).

Even though the names appear similar, certificate names are **case-sensitive**. A mismatch like this breaks the link between Core and OCM, triggering the alert.

## [**Resolution:**](/docs/myop/knowledge-base/why-does-my-opswat-central-managemant-v8-show-a--significant-iss#resolution)

To resolve the mismatch, follow these steps **in MetaDefender Core UI**:

1. **Unenroll the Affected Core**

- In **MetaDefender Core UI** > Click on **Managed**
- Click **Unenroll**.

2. **Temporarily Disable Batch Signing**

- Go to **Workflow Management > Workflows**
- Select the affected workflow (e.g., **Kiosk**).
- In the **General** tab, uncheck **“Use certificate to generate batch signature.”**

- ** Save changes **

3. **Correct the Certificate Name**

- Go to **Inventory > Certificates**.
- Either rename the existing certificate to match OCM (e.g., `"manifestcert"`) or add a new certificate with the correct name.
- 4. **Re-enable Batch Signing**
- Return to **Workflow Management > Workflows**.
- Open the workflow.
- Re-enable **“Use certificate to generate batch signature.”**
- Select the correctly named certificate (e.g., `"manifestcert"`).

- ** Save changes. **

5. **Re-enroll** **MetaDefender Core**

Check [this link](https://www.opswat.com/docs/product-management/configuration) to see how to enroll a Core instance into OCM8

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
