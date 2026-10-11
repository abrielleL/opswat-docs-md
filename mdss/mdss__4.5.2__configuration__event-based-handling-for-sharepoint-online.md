<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/event-based-handling-for-sharepoint-online -->

# Event-based handling for SharePoint Online

MetaDefender Storage Security supports event-based handling for SharePoint Online, enabling real-time scanning of content as it is added.

Unlike other storage providers, **MDSS automates the setup of the Microsoft Graph subscriptions** needed for monitoring SharePoint events. This makes the configuration process simpler and faster for SharePoint Online users.

## **Advantages**

- MDSS automatically creates, renews, and manages all necessary Microsoft Graph API subscriptions. **No manual intervention is required for this critical infrastructure**
- Get real-time scanning up and running faster, without the complexities of manual Graph API configuration
- Files are scanned immediately upon upload or modification in SharePoint Online, providing continuous security

## **How it works**

MDSS leverages Microsoft Graph API webhooks to receive notifications from SharePoint Online whenever content is added or modified. MDSS handles the entire lifecycle of these webhook subscriptions on your behalf. For this to work correctly, your MDSS instance must be reachable from the internet to receive these notifications from Microsoft.

## **Prerequisites**

Before MDSS can automatically configure event-based handling, your environment must meet the following crucial prerequisites:

1. MDSS Hosted and Accessible via [HTTPS](https://docs.opswat.com/mdss/configuration/enabling-https)
   - SharePoint Online sends event notifications (webhooks) to your MDSS instance. These notifications require a secure HTTPS connection to a trusted endpoint
   - Your MDSS instance must be served over HTTPS
   - The machine running MDSS needs a valid SSL certificate from a trusted Certificate Authority. While self-signed certificates can technically work, they are **strongly discouraged** as they require complex trust configurations within your SharePoint environment and can lead to notification failures if not managed perfectly
2. Publicly Accessible MDSS Port
   - Microsoft Graph API needs to send event notifications directly from Microsoft's cloud services to your MDSS instance. If MDSS is not publicly accessible, these critical notifications cannot be delivered
   - The HTTPS port used by MDSS (default is `443`) must be open and reachable from the public internet
   - Configure your firewall, router, load balancers, and any other network security infrastructure to allow incoming HTTPS traffic on this port, directing it to the MDSS host machine
3. Configured SharePoint Online Connection in MDSS
   - MDSS needs to authenticate with your SharePoint Online environment to register the webhooks for event notifications and access file content for scanning
   - Your SharePoint Online storage must be successfully added and properly configured within MDSS.
   - Make sure that MDSS has the necessary permissions to access your SharePoint site(s). These permissions are typically granted via OAuth during the initial storage addition process and must include the ability to manage Graph API subscriptions for the targeted resources

> **Warning**
>
> The document library’s display name must match its name in the web address (URL). For example, if the URL is `.../sites/[SiteName]/[LibraryName]/`, the name should also be **[LibraryName]**. If they differ, SharePoint event-based handling will not work, and MDSS won’t process file events for that library.

Once these prerequisites are met, MDSS will automatically handle the setup and ongoing management of event-based scanning for your configured SharePoint Online storage

## Unsupported SharePoint Content Types

Certain SharePoint content types fall outside the scope of items protected by our solution. Administrators should be aware of the following exclusions when reviewing coverage of their SharePoint environments.

### Form Templates Library

The **Form Templates** library that appears under a SharePoint site's contents is a hidden system library automatically provisioned by SharePoint on every site. Despite its visibility in the site contents view, it is not a standard document library and is not backed by a Drive resource in Microsoft Graph. As a result, this library is **not protected** by our solution.

### Lists

SharePoint items of type **List** (for example, custom lists, task lists, and contact lists) are not backed by a Drive resource in Microsoft Graph and are therefore **not protected** by our solution.

### Site Pages and Other Page Libraries

Content stored in libraries of type **Page Library** (such as the default *Site Pages* library) is **not protected** by our solution. These libraries host SharePoint pages rather than user documents and are managed through SharePoint's page infrastructure rather than as standard document storage.

| Content Type | Microsoft Graph Drive | Protected |
| ---- | ---- | ---- |
| Document Library | Yes | Yes |
| Form Templates (system library) | No | No |
| List | No | No |
| Page Library (e.g., Site Pages) | No | No |

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
