<!-- source: https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/knowledge-base/how-do-i-clear-out-my-metadefender-kiosk-linux-license-key- -->

# How do I clear out my MetaDefender Kiosk Linux license key?

This article applies to all MetaDefender Kiosk Linux versions.

In order to clear out the license for your MD Kiosk Linux deployment using API calls, you will need the following variables:

1. Obtain your valid License/Activation Key.
2. Obtain your Deployment ID.

Apply the following API call, as illustrated in the screenshot below:

BashCopycurl -X GET https://activation.dl.opswat.com/deactivation?key=<activation-key>&deployment=<deployment unique-ID>  

- Once the API call is done and you get the “200” response you should be able to use the license to activate different deployments if needed.
- Please take note that this API call will remove all licensed MD Kiosk Linux deployments from the activation key (all deployments will become unlicensed).

Support:

If you have any difficulty Deactivating MetaDefender Kiosk Linux Via API Calls, please follow these instructions on [How To Create a Support Package](https://www.opswat.com/docs/mdkiosk-linux/troubleshooting), before logging a [Support Ticket](https://my.opswat.com/support) with the OPSWAT team.
