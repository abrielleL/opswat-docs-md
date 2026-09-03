<!-- source: https://www.opswat.com/docs/mdss/configuration/event-based-handling -->

# Event-based handling

Event-based real-time processing triggers scans immediately upon file creation or modification notifications.

This method is supported for the following storage units: **Amazon S3**, **S3 Compatible**, **Azure Blob**, **Alibaba Cloud**, **Google Cloud**, **Box**, **SMB Compatible**, **NFS**, **SFTP, FTP**, **SharePoint Online** and **NetApp ONTAP**.

## [Generic Webhook Endpoint](/docs/mdss/configuration/event-based-handling#generic-webhook-endpoint)

MetaDefender Storage Security provides a generic webhook endpoint **http(s)://{baseurl}/api/webhook/realtime** for integration with serverless functions from AWS, Azure, Alibaba Cloud, and Google Cloud Platform.

Important Note for BOX Integration

For Box, the API endpoint is `https://{baseurl}/api/webhook/realtime/public/{storageClientId}.` The generic webhook endpoint is **NOT** compatible with BOX. Refer to the [Event-based handling for Box](/docs/mdss/configuration/event-based-handling-for-box) documentation for specific instructions.

## [Integrating Cloud Provider Event Notifications](/docs/mdss/configuration/event-based-handling#integrating-cloud-provider-event-notifications)

To integrate event notifications from AWS, Azure, Alibaba Cloud, and Google Cloud Platform with MetaDefender Storage Security's real-time processing, the following parameters must be included as request headers in the event payload:

- `storageclientid` - Obtain this value from the Dashboard, once you select the Storage Unit desired

- `apikey`- Generate an API key for authentication in MetaDefender Storage Security under "Settings" -> "Users" -> "User (More Options)." Refer to the "[Generate an API Key](/docs/mdss/configuration/generate-an-api-key)" documentation for detailed instructions.
- `apiendpoint`- Use the generic real-time webhook endpoint: `http(s)://{baseurl}/api/webhook/realtime`

For examples of the request format, please visit [this page](/docs/mdss/configuration/event-based-request-format).

For detailed configuration instructions, please consult the [Event-Based Real-Time Cloud Functions Examples](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) documentation.
