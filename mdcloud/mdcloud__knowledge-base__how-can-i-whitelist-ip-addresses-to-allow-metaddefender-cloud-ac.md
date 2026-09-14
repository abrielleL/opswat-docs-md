<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/how-can-i-whitelist-ip-addresses-to-allow-metaddefender-cloud-ac -->

# How can I whitelist IP addresses to allow MetaDdefender Cloud access to my storage service

This article applies to all active MetaDefender Cloud license holders - whether your product is paid for or issued for evaluation purposes.

If you're encountering [upload errors](https://www.opswat.com/docs/mdcloud/v-4/integrations/errors#error-codes-explained) such as:

Info

400146 – Provided download URL is not valid or inaccessible

This typically occurs when MetaDefender Cloud attempts to retrieve a file from a private or restricted storage source (e.g., AWS S3, Wasabi, Azure Blob, Google Cloud, or an on-prem file server), but is blocked due to network or access restrictions.

To resolve this, ensure that your storage service allows external access from MetaDefender Cloud. Many cloud storage solutions are secured by default and require explicit whitelisting. You may need to update your firewall or access control settings to allow inbound requests from MetaDefender Cloud's IP addresses.

To proceed, please **submit a support case to OPSWAT** with the following information:

- Your storage service type (e.g., S3, Azure Blob, FTP, etc.)
- Confirmation that IP-based access control is in place
- Details about the access method (API, URL, or protocol)
- Any error messages or logs you’ve observed

OPSWAT Support will provide you with the appropriate list of IP addresses based on your region and deployment, and guide you through the necessary steps to enable secure access.

Note:

IP addresses may differ depending on how MetaDefender Cloud is hosted (cloud or on-prem) and where your storage service is located.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
