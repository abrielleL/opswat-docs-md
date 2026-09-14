<!-- source: https://www.opswat.com/docs/md-ot-security/operating/recommendation -->

# Recommendation

The **Recommendation** card sits on an asset's **Risk Score** tab (inside the asset-detail modal) and shows AI-generated remediation guidance for that specific device.

## [Enabling the feature](/docs/md-ot-security/operating/recommendation#enabling-the-feature)

Risk Recommendation is controlled by a site-scoped toggle. To turn it on:

1. From the Recommendation card, click **Application Settings** in the "Manage recommendation on Application Settings" line — this closes the asset-detail modal, switches the active region to the device's site, and opens **Settings**.
2. On the **Application** tab, scroll to **AI-Powered Enablement Settings**.
3. Turn on **Risk Recommendation** and click **Save**.

The manage link above is always shown, even when the feature is off or the viewer has no read access — only the recommendation body underneath it is gated. This lets any viewer reach the toggle without needing someone else to enable it for them first.

## [Gating behavior](/docs/md-ot-security/operating/recommendation#gating-behavior)

| Condition | Manage link | Recommendation body |
| --- | --- | --- |
| Feature enabled and viewer has Recommendation read access | Shown | Shown |
| Feature disabled, or viewer has no Recommendation read access | Shown | Hidden |

Recommendation read access is controlled by its own access-control feature, **Recommendation (Asset Detail)**, under the **Asset** feature group — it is independent from Vulnerability access, so an admin can grant or revoke it separately.

## [Viewing a recommendation](/docs/md-ot-security/operating/recommendation#viewing-a-recommendation)

Once the feature is enabled and the card body is visible, click **AI Recommendation** to open the full text in a modal.

- The first time a device's recommendation is requested, the system runs a real AI analysis and shows an **"Analyzing for recommendation..."** loading state while it works.

- When generation finishes, the modal fills in with the full recommendation text and a toast notification confirms completion.
- The **Recommendation** title has an info icon explaining what the text is: "AI-generated remediation guidance for this asset based on its detected vulnerabilities."

- Devices with no detected vulnerabilities skip AI analysis entirely and return a canned message immediately: "No known vulnerabilities were found for this device based on current CVE data. No remediation action is required at this time."

### [Caching](/docs/md-ot-security/operating/recommendation#caching)

Recommendations are cached server-side per device:

- Reopening the same device and clicking **AI Recommendation** again returns the identical text instantly, without re-running analysis.
- If a generation job is still running when the card is reopened, the loading spinner appears immediately rather than the job restarting.

### [Background generation and notifications](/docs/md-ot-security/operating/recommendation#background-generation-and-notifications)

Closing the recommendation modal's own **X** does **not** cancel an in-progress generation — it keeps running in the background. A row for the device appears in the notification bell once the job completes, so a viewer can close the modal and come back to it later. Clearing a row from the bell only removes the notification; it does not delete the cached recommendation.

## [Access control](/docs/md-ot-security/operating/recommendation#access-control)

The recommendation body — and the API call that fetches it — is protected by a dedicated **risk-recommend** feature (view action **view-risk-recommend-asset**) rather than reusing the Vulnerability feature. It defaults to disabled and is scoped per site, so an admin can grant recommendation access to some users without also granting vulnerability access.
