<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-do-i-activate-deactivate-a-metadefender-core-deployment-via- -->

# How do I activate/deactivate a MetaDefender Core Deployment via API calls?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Please Note:

In order to activate/deactivate your MetaDefender Core deployment via API calls, you will need to:

1. Obtain your valid **License/Activation Key**.
2. Obtain your **Deployment ID**.
3. Use these details to apply the relevant **API Calls** listed below.

To obtain the above mentioned details via API, please [Read This](https://docs.opswat.com/mdcore/metadefender-core/ref#licenseget).

## [Activate your deployment via API](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-activate-deactivate-a-metadefender-core-deployment-via-#activate-your-deployment-via-api)

Apply the following API call, as illustrated in the screenshot below:

BashCopycurl -X GET "https://activation.dl.opswat.com/activation?key=<activation-key>&deployment=<deployment unique-ID>&quantity=<quantity>"

**After running the API call described above users will need to use the “save response file” option and use the .yml file to activate the Core deployment.**

## [Deactivate your deployment via API](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-activate-deactivate-a-metadefender-core-deployment-via-#deactivate-your-deployment-via-api)

Apply the following API call, as illustrated in the screenshot below:

BashCopycurl -X GET "https://activation.dl.opswat.com/deactivation?key=<activation-key>&deployment=<deployment unique-ID>"

**After running the API call described above the mentioned deployment will be removed from the activation key.**

Support:

If you have any difficulty **Activating or Deactivating a MetaDefender Core Deployment Via API Calls**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
