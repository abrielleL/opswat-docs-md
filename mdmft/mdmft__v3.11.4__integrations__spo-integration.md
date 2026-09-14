<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/integrations/spo-integration -->

# SPO Integration

Summarize Page    Connect to Cursor Connect to VS Code Trademark Notice

SharePoint Online™ (referred to as "SPO" in this documentation) is a registered trademark of Microsoft Corporation.

This section covers the integration of SPO document libraries with MetaDefender Managed File Transfer for various use cases, such as automating file transfers. For example: [Introduction to File Transfer Automation](/docs/mdmft/v3.11.4/automated-file-transfer/automated-jobs).

## [MetaDefender MFT in Microsoft® Entra ID](/docs/mdmft/v3.11.4/integrations/spo-integration#metadefender-mft-in-microsoft-entra-id)

1. Register MetaDefender MFT

Before integrating SPO with MetaDefender® MFT, you must register MetaDefender® MFT in Microsoft® Entra ID.

2. Set API permissions

MetaDefender® MFT uses the Microsoft® Graph API to access SPO document libraries as a Microsoft® Cloud service resource. To enable API usage, you need to grant the necessary permissions to the registered MetaDefender® MFT application with Microsoft® Entra ID.

3. In the API permissions section of the registered MetaDefender® MFT application in Microsoft® Entra ID, add the following **Microsoft Graph** **application** permissions for SPO:

- For pull jobs only: **Sites.Read.All**
- For both pull and push jobs, or push jobs only: **Sites.ReadWrite.All**

App registration's API permissions

## [Integrating SPO with MetaDefender MFT](/docs/mdmft/v3.11.4/integrations/spo-integration#integrating-spo-with-metadefender-mft)

To manage SPO integration instances, go to "Settings" → "Integrations" → "SPO".

SPO integrations are globally available, meaning all users with the appropriate permissions can view the same set of integrations.

## [Configuration](/docs/mdmft/v3.11.4/integrations/spo-integration#configuration)

1. To add a new SPO Integration, click the "Add SPO Integration" button.

- SPO Name: The display name, customizable as needed. This name will be used when selecting the integration instance.
- Environment Type: Choose the appropriate environment based on your organization’s SharePoint SPO configuration:

  - Azure Commercial (Default): Most organizations use this option. It connects to .com endpoints such as [login.microsoftonline.com](http://login.microsoftonline.com/), [http://graph.microsoft.com](http://graph.microsoft.com/) , and [http://sharepoint.com](http://sharepoint.com/).
  - Azure Government: Select this if your SharePoint URL ends with .sharepoint.us or if your organization operates in a U.S. Government environment. This connects to .us endpoints such as [login.microsoftonline.us](http://login.microsoftonline.us/), [http://graph.microsoft.us](http://graph.microsoft.us/) , and [sharepoint.us](http://sharepoint.us/).
- Site URL: The URL of the SPO site. To locate the URL, you can:

  - Go to the "SharePoint admin center" → "Active sites" → Locate the desired SPO site → Copy its URL.
  - Go to the SPO site and copy the *site portion* from the browser's address bar. The URL should resemble: <https://mycompany.sharepoint.com/sites/MySite>
- Document Library: The name of the document library, which can be found in the left pane of the SPO site. Each integration is limited to a single document library, which will serve as the root path for automated jobs.
- Tenant ID: The unique identifier for the Microsoft Entra ID instance where MetaDefender MFT is registered. This can be found in the "Azure Portal" under the "Entra ID" section.

## [Test Connection](/docs/mdmft/v3.11.4/integrations/spo-integration#test-connection)

You can test the connection for a configured SharePoint Online (SPO) integration by following these steps.

**Please note**: You will need to provide the credentials of MetaDefender® MFT you want to test with. MetaDefender MFT will not store these credentials, they are used only for validation during this test.

1. Click action menu [three dot] → click "Test Connection"
2. Popup opens → Select credential type:

   - Client Secret *(default)* or Certificate
3. Enter required fields:

   - Client Secret: Client ID + Client Secret.
   - Certificate: Client ID + Cert Id.
4. Click "Test Connection" button.
5. MFT runs tests and shows results

The Test Connection process validates your SPO configuration by checking:

- Environment Type & Site URL: Confirms the URL points to a valid SharePoint site and matches the selected environment.
- Document Library: Ensures the specified library exists within the site.
- Tenant ID: Verifies the provided Microsoft Entra ID tenant is valid.
- Credentials & Permissions: Confirms credentials have sufficient rights to pull and push files in the document library.

Your SharePoint Online™ integration with MetaDefender® MFT is now complete. Learn how to configure Automated Jobs using this integration by reading more [here](/docs/mdmft/v3.11.4/metadefender-managed-file-transfer/v3.11.0/automated-file-transfer/spo-push-files).
