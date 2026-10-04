<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-is-the-locally-configured-metadefender-kiosk-certificate-not -->

# Why is the locally configured MetaDefender Kiosk certificate not included when I import a Kiosk configuration into a My OPSWAT Central Management policy?

> **Check Your Version:** This article applies to My OPSWAT Central Management version 10.x and later, managing MetaDefender Kiosk instances.

## **Issue**

You import an existing MetaDefender Kiosk configuration into a My OPSWAT Central Management policy and assign that policy to a group. The certificate that was previously configured on the Kiosk console is not carried over with the rest of the configuration, and the certificate selection on the Kiosk appears cleared after the policy is applied.

## **Possible Causes**

This is expected behavior rather than a defect. It occurs when all of the following are true:

- The certificate was uploaded directly on the Kiosk console, which makes it a **local** certificate. Local certificates are stored and managed on the Kiosk itself and appear with an **Unmanaged** status in the instance's **Certificates** tab.
- My OPSWAT Central Management does not copy locally managed certificates from a Kiosk instance up to the central server. This is intentional — it prevents certificate and private key material from being uploaded to the server without an administrator explicitly choosing to do so.
- Because the certificate does not exist as a centrally managed certificate on the server, it cannot be included in the imported configuration or in the policy. Only certificates listed in the policy's **Certificates** tab can be selected, so the policy applies with no certificate assigned.

## **Resolution**

To use a certificate with a centrally managed Kiosk, import the certificate into My OPSWAT Central Management and assign it to the Kiosk instances or to the policy.

Full details on certificate management are available in the [My OPSWAT Central Management documentation](https://www.opswat.com/docs/cm/configurations/certificates-management).

### **Steps to verify the assignment**

1. Open the **Certificate Details** page and select the **Distribution** tab. The Kiosk instance or policy is listed with a **Management Status** of **Assigned**.
2. On the Kiosk, go to **Inventory → Devices → Certificates** tab and confirm the certificate is listed as managed rather than **Unmanaged**.

## **Recommendation**

For any Kiosk you intend to manage centrally, import the certificate into My OPSWAT Central Management first and assign it from there, rather than uploading it on the Kiosk console. Centrally managed certificates survive policy changes, can be reassigned without touching each Kiosk, and show their distribution status in one place.

Note that **Force Unassign** does the reverse: it removes the certificate from My OPSWAT Central Management immediately, and the copy left on the Kiosk becomes a locally managed certificate again that can no longer be controlled centrally.

> **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
