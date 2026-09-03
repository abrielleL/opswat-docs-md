<!-- source: https://www.opswat.com/docs/mdmft/integrations/spo-add-in-integration -->

# SPO Add-in Integration

Summarize Page    Connect to Cursor Connect to VS Code Trademark Notice

SPO Add-in Integration (referred to as "SPOA" in this documentation) is a registered trademark of Microsoft Corporation.

This section covers the integration of SPO Add-in into MFT.

## [MetaDefender MFT in Microsoft® Entra ID](/docs/mdmft/integrations/spo-add-in-integration#metadefender-mft-in-microsoft-entra-id)

1. Register MetaDefender MFT

Before integrating SPO with MetaDefender® MFT, you must register MetaDefender® MFT in Microsoft® Entra ID.

2. Set API permissions

MetaDefender® MFT uses the Microsoft® Graph API to access SPO document libraries as a Microsoft® Cloud service resource. To enable API usage, you need to grant the necessary permissions to the registered MetaDefender® MFT application with Microsoft® Entra ID.

3. In the API permissions section of the registered MetaDefender® MFT application in Microsoft® Entra ID, add the following **Microsoft Graph** **application** permissions for SPO:

- For pull jobs only: **Sites.Read.All**
- For both pull and push jobs, or push jobs only: **Sites.ReadWrite.All**

App registration's API permissions

## [Setup SPO Add-in at MetaDefender MFT](/docs/mdmft/integrations/spo-add-in-integration#setup-spo-add-in-at-metadefender-mft)

To manage SPO integration instances, go to "Settings" → "Integrations" → "SPO Add-in".

SPOA integrations are globally available, meaning all users with the appropriate permissions can view the same set of integrations.

### [SharePoint Online Add-in](/docs/mdmft/integrations/spo-add-in-integration#sharepoint-online-add-in)

This section contain the switch that will let admin user enable/disable request from your SharePoint site.

#### [Configuration](/docs/mdmft/integrations/spo-add-in-integration#configuration)

This section let will require you input your company SharePoint site information, and the credential that MFT will use to access the SharePoint resource.

- Environment Type: Choose the appropriate environment based on your organization’s SharePoint SPO configuration:

  - Azure Commercial (Default): Most organizations use this option. It connects to .com endpoints such as [login.microsoftonline.com](http://login.microsoftonline.com/), [http://graph.microsoft.com](http://graph.microsoft.com/) , and [http://sharepoint.com](http://sharepoint.com/).
  - Azure Government: Select this if your SharePoint URL ends with .sharepoint.us or if your organization operates in a U.S. Government environment. This connects to .us endpoints such as [login.microsoftonline.us](http://login.microsoftonline.us/), [http://graph.microsoft.us](http://graph.microsoft.us/) , and [sharepoint.us](http://sharepoint.us/).
- Site URL: The URL of the SPO site. To locate the URL, you can:

  - Go to the "SharePoint admin center" → "Active sites" → Locate the desired SPO site → Copy its URL.
  - Go to the SPO site and copy the *site portion* from the browser's address bar. The URL should resemble: <https://mycompany.sharepoint.com/sites/MySite>
- Tenant ID: The unique identifier for the Microsoft Entra ID instance where MetaDefender MFT is registered. This can be found in the "Azure Portal" under the "Entra ID" section.
- Client ID: The Client ID is listed in the 'Overview' section of App registrations.
- Client Secret: The Client Secret is listed in the 'Certificates & secrets' section of App registrations.

#### [Test Connection](/docs/mdmft/integrations/spo-add-in-integration#test-connection)

You can test the connection for a configured SharePoint Online (SPO) integration by following these steps.

**Please note**: You will need to provide the Document Library name of MetaDefender® MFT you want to test with.

- Document Library: The name of the document library, which can be found in the left pane of the SPO site. Each integration is limited to a single document library, which will serve as the root path for automated jobs.

The Test Connection process validates your SPO configuration by checking:

- Environment Type & Site URL: Confirms the URL points to a valid SharePoint site and matches the selected environment.
- Document Library: Ensures the specified library exists within the site.
- Tenant ID: Verifies the provided Microsoft Entra ID tenant is valid.
- Credentials & Permissions: Confirms credentials have sufficient rights to pull and push files in the document library.

Your SharePoint Online™ integration with MetaDefender® MFT is now complete. Learn how to configure Automated Jobs using this integration by reading more [here](/docs/mdmft/automated-file-transfer/spo-push-files).

#### [Download Add-in](/docs/mdmft/integrations/spo-add-in-integration#download-add-in)

This section will let you download the OPSWAT MetaDefender File Transfer SharePoint Add-in. This is client package that will seamlessly help you interact with MFT right from your SharePoint site.

The package file is: **mft-spoa.sppkg**

## [Setup SPO Add-in at your company SharePoint site](/docs/mdmft/integrations/spo-add-in-integration#setup-spo-add-in-at-your-company-sharepoint-site)

This section will guide admin user how to setup and apply the SPO Add-in to your company SharePoint site.

### [Publish to your company SharePoint Store site](/docs/mdmft/integrations/spo-add-in-integration#publish-to-your-company-sharepoint-store-site)

Go to Manage Apps page of your tenant, the url would be similar to this:

`https://**yourtenantdomain**.sharepoint.com/sites/appcatalog/_layouts/15/tenantAppCatalog.aspx/manageApps`

Upload the **mft-spoa.sppkg** file to Manage apps site.
The app name is **OPSWAT MetaDefender File Transfer SharePoint Add-in**.

Enable app: A right modal will show up after you upload the package to guide you enable the app
Tips: Select the "Only enable this app" then manually apply it to your specific site later. This will save your time on the whole deployment process.

Approve access so this app works as designed.
Tips: Click "Go to API access page" then follow the guideline from SharePoint to grant appropriate permissions.

View app: close the right modal then select the app row and click "View app details"

At this point, the app has been published successfully to your company SharePoint store.

### [**Install to your company site**](/docs/mdmft/integrations/spo-add-in-integration#install-to-your-company-site)

After deploy the app to SharePoint store, this section will guide you how to install the app to your site.

Go to your "Site Content" site then click "New" and select "App",
This action will guide you to the SharePoint store, then you can install the app

At My apps: select "From my organization" filter, you will see all apps that you can install to your site

Click "Add", now the OPSWAT MetaDefender File Transfer SharePoint Add-in app has been installed to your site successfully

Double check: go back to your "Site Contents" page, you will see there are two item has been added to your site.
MFT_Configuration: this contain the configuration of the app
OPSWAT MetaDefender File Transfer SharePoint Add-in: this is the main application

### [Configure for the first use](/docs/mdmft/integrations/spo-add-in-integration#configure-for-the-first-use)

**Prerequisites**: your SharePoint account need to have the SharePoint Administrator role, you can configure this role for your account at <https://portal.azure.com>

**Configure the OPSWAT Add-in:**

After installing the app on your site, open any Document Library to begin the configuration. This step allows the SharePoint app to identify which MFT Server it should connect to.

In this instruction, I will use "library with spaces" as a sample Document Library.

At command bar, click "..." (three dots) icon button, then click "Configure OPSWAT Add-in" button

Input the MFT Server Address and click Save. This configuration will be applied for all Document Library in your site.

## [Transfer SharePoint file securely with MetaDefender MFT](/docs/mdmft/integrations/spo-add-in-integration#transfer-sharepoint-file-securely-with-metadefender-mft)

This section to guide normal user transfer file securely with SharePoint Add-in.

Right click to any file that you want to share, then click to "Secure share via OPSWAT"

A login modal will show up if you haven't logon yet

Enter users and groups that you want to share this file, notify them with a message if need. Then click Share

During the process, it may take long because of the size of the file or many reason... You can hide the progress modal by click the Hide button, and click the "View active progress" to show it back

A file is uploaded, scanned (if configured) and shared successfully. Click "View file in MFT" to view it
