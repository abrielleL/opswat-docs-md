<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run- -->

# Why Am I Seeing the Error “Stripe Checkout Is Not Able to Run in an iFrame”?

## [Overview](/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run-#overview)

If you see the message below when trying to complete a purchase, Stripe Checkout is being blocked because it’s being launched from within an embedded page (an **iframe**) instead of a normal browser tab (a **top-level window**):

> **“Stripe Checkout is not able to run in an iFrame. Please redirect to Checkout at the top level.”**

Stripe Checkout **does not support running inside iframes**. This is expected behavior enforced by Stripe for security and reliability.

---

## [What you may notice (symptoms)](/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run-#what-you-may-notice-symptoms)

- Clicking **Buy / Upgrade / Checkout** does nothing, or the page briefly flashes and returns.
- The issue reproduces across browsers (Chrome/Safari), including incognito/private mode.
- Clearing cookies/cache and disabling extensions does not help.
- The browser console shows: `Stripe Checkout is not able to run in an iFrame. Please redirect to Checkout at the top level.`

---

## [Why this happens](/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run-#why-this-happens)

The most common scenario is opening the store or licensing flow through **My OPSWAT Portal (MOP)** (or another portal/container) that **renders pages inside an iframe**.

When the checkout flow is started inside an iframe, Stripe blocks it and shows the error above because Checkout must be opened via a **top-level redirect**.

---

## [Workaround (recommended)](/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run-#workaround-recommended)

Open the MD Cloud store directly in a new browser tab (outside of the portal/iframe), then start checkout again:

**Direct link (MD Cloud store):** [Licensing | MetaDefender Cloud](https://metadefender.opswat.com/store)

### [Steps](/docs/mdcloud/knowledge-base/why-am-i-seeing-the-error----stripe-checkout-is-not-able-to-run-#steps)

1. Copy the link above.
2. Paste it into a **new browser tab**.
3. Re-initiate the purchase/checkout.

**Expected result:** Stripe Checkout opens as a full-page, top-level checkout and completes normally.

Support:

If Further Assistance is required, please log a [support case or chat with our support engineer](https://my.opswat.com/support).
