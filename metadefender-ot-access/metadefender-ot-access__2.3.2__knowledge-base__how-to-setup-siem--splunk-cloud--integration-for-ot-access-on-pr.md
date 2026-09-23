<!-- source: https://www.opswat.com/docs/metadefender-ot-access/2.3.2/knowledge-base/how-to-setup-siem--splunk-cloud--integration-for-ot-access-on-pr -->

[MetaDefender OT Access](https://www.opswat.com/docs/metadefender-ot-access/overview)Need Help?
# How to setup SIEM (Splunk Cloud) integration for OT Access On-premise?

This article applies to OT Access releases deployed on-premise

This article provides detailed instructions for setting up Splunk SIEM on the cloud. OT Access will be integrated with Splunk using the HTTP Event Collector (HEC).

### [Preparing Splunk on Cloud](/docs/metadefender-ot-access/2.3.2/knowledge-base/how-to-setup-siem--splunk-cloud--integration-for-ot-access-on-pr#preparing-splunk-on-cloud)

- Step 1: Login to your Splunk Cloud instance.
- Step 2: Go to Settings > Data Input (we will create a new data input for OT Access)

- Step 3: You need to select correct Input type (HEC - HTTP Event Collector)

- Then, you need to input to the field as example below.

- After finish creating, you can back to HTTP Event Collector to check your new token will be there.

### [Setting up in OTA](/docs/metadefender-ot-access/2.3.2/knowledge-base/how-to-setup-siem--splunk-cloud--integration-for-ot-access-on-pr#setting-up-in-ota)

After we have the token, we will access to OT Access Management to setup SIEM with **superadmin** user.

Then, go to “Settings” > “Integration”, we will see the setting for SIEM

In this page, you need to input the correct information

- **Server**: this should be domain of your Splunk instance.

HtmlCopyhttps://<Splunk_Instance>.splunkcloud.com

- **HEC Token**: You can get this from your Splunk

- **Index**: Please ensure that you enter the correct “Index” configured in your HEC token settings in Splunk. For example, if the index for your token is set to “main”, then the Index field in the SIEM settings should also be “main”.
- **Source Type:** It depends on your HEC token configuration in Splunk. If you've specified a Source Type, you’ll need to enter it accordingly. Otherwise, you can leave it blank, as shown in the example above.
- **Host**: This should be the hostname for the machine originating the events, in this case MetaDefender OT Access instance.

After entering all the required information, click the “Test Connection” button to verify the configuration.

If OT Access successfully connects to your Splunk instance, you will see the results displayed. Then, click the “Save” button to proceed.

Now, return to your Splunk instance and search for the hostname “MetaAccessOT” to verify that logs are being received from OT Access.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
