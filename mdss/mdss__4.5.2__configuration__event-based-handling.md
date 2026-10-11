<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/event-based-handling -->

# Event-based handling

> **Event-Based File Discovery**
>
> Event-based real-time processing triggers scans immediately upon file creation or modification notifications.
>
> This method is supported for the following storage units: **Amazon S3**, **S3 Compatible**, **Azure Blob**, **Alibaba Cloud**, **Google Cloud**, **Box**, **SMB Compatible**, **NFS**, **SFTP, FTP**, **SharePoint Online** and **NetApp ONTAP**.

## Generic Webhook Endpoint

MetaDefender Storage Security provides a generic webhook endpoint **http(s)://{baseurl}/api/webhook/realtime** for integration with serverless functions from AWS, Azure, Alibaba Cloud, and Google Cloud Platform.

> **Important Note for BOX Integration**
>
> For Box, the API endpoint is `https://{baseurl}/api/webhook/realtime/public/{storageClientId}.`  The generic webhook endpoint is **NOT** compatible with BOX. Refer to the [Event-based handling for Box](https://www.opswat.com/docs/mdss/configuration/event-based-handling-for-box) documentation for specific instructions.

## Integrating Cloud Provider Event Notifications

To integrate event notifications from AWS, Azure, Alibaba Cloud, and Google Cloud Platform with MetaDefender Storage Security's real-time processing, the following parameters must be included as request headers in the event payload:

- `storageclientid` - Obtain this value from the Dashboard, once you select the Storage Unit desired

![](https://uploads.developerhub.io/prod/k8zL/27xk3mj2yb90vkynvl3q1t8zgh4eb2fxkc7xqlaj4h2tneplqmh4rv3whoz69vn6.png)

- `apikey`- Generate an API key for authentication in MetaDefender Storage Security under "Settings" -> "Users" -> "User (More Options)." Refer to the "[Generate an API Key](https://www.opswat.com/docs/mdss/configuration/generate-an-api-key)" documentation for detailed instructions.
- `apiendpoint`- Use the generic real-time webhook endpoint: `http(s)://{baseurl}/api/webhook/realtime`

For examples of the request format, please visit [this page](https://www.opswat.com/docs/mdss/configuration/event-based-request-format).

For detailed configuration instructions, please consult the [Event-Based Real-Time Cloud Functions Examples](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples) documentation.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
