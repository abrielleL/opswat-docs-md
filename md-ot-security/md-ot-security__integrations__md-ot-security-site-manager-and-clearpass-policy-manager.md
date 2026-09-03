<!-- source: https://www.opswat.com/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager -->

# MetaDefender OT Security and HPE Aruba Networking ClearPass Integration

## [Introduction](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#introduction)

This Integration Guide provides detailed instructions on configuring and utilizing the integration between MetaDefender OT Security and HPE Aruba Networking ClearPass Policy Manager. MetaDefender OT Security offers unparalleled visibility, continuous monitoring of threats and vulnerabilities, and in-depth insights into Industrial Control Systems (ICS) networks.

This initial phase of integration focuses on MetaDefender OT Security's capability to detect, discover, and classify OT/ICS endpoints, sharing this classification directly with ClearPass Policy Manager through the ClearPass Security Exchange framework and exposed open APIs. MetaDefender OT Security will automatically populate the ClearPass Policy Manager endpoint database with endpoint classification data and a range of custom security attributes.

This guide focuses on Phase 1 of our planned integration with ClearPass Policy Manager, which provides centralized visibility of network assets and endpoints across both IT and OT infrastructures. This unified platform enables the definition and enforcement of comprehensive endpoint and edge security policies. Stay tuned for updates as we continue to expand and enhance this integration framework.

## [Pictorial view of the Integration](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#pictorial-view-of-the-integration)

The diagram below provides an overview of the components and their interactions

Pictorial view of MetaDefender OT Security and ClearPass Policy Manager integration:

## [ClearPass Policy Manager Configuration](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#clearpass-policy-manager-configuration)

### [1. Create a ClearPass Policy Manager User](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#1-create-a-clearpass-policy-manager-user)

Create a user from **ClearPass Policy Manager** > **Administration -> Users and Privileges -> +ADD -> {Create a user, ensure that you use a privilege level of API Administrator}**

Create an API-level account in ClearPass

### [2. Create an Operator Profile](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#2-create-an-operator-profile)

**ClearPass Guest > Administration > Operator Logins > Profiles.**

Click on “Create a new operator profile” on the top right corner of the page and define an operator profile as shown below

Pick and choose the necessary access for MetaDefender OT Security to update the ClearPass Policy Manager endpoint database with the device context. In summary, all options are set as ‘No Access’ except for the following.

For API Services, select Custom and then grant the following access

• **Allow API Access = Allow Access**

For Policy Manager, select Custom and then grant the following access

**• Dictionary – Attributes = Read, Write, Delete**

**• Dictionary – Fingerprints = Read, Write, Delete**

**• Identity – Endpoints = Read, Write, Delete**

Operator Profile - Access restrictions 1

Operator Profile - Access restrictions 2

Operator Profile - Access restrictions 3

### [3. Create an API Client](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#3-create-an-api-client)

**ClearPass Guest > Administration > API Services > API Clients > {Create API Client}**

Notice the highlighted configuration options needed, and set them as appropriate

• Operating Mode = ClearPass REST API – Client will be used for API calls to ClearPass Policy Manager

• Operator Profile = Use the Operator Profile created previously

• Grant Type = Client credentials (grant_type=client_credentails)

Create an API Client

At this time all of the necessary config has been created in Policy Manager, ensure you have the below list of information collected before proceeding to the next section.

- ClearPass Policy Manager API Administrator User ID
- ClearPass Policy Manager API Administrator User Password
- ClearPass Policy Manager OAuth2 API Client NAME
- ClearPass Policy Manager OAuth2 API Client Secret

## [MetaDefender OT Security Configuration:](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#metadefender-ot-security-configuration)

For this initial integration between the two products, there is limited configuration necessary on MetaDefender OT Security. After the configuration is complete the MetaDefender OT Security will update the ClearPass Policy Manager endpoint database as it discovers new endpoints periodically. Follow the steps below to configure and enable this integration.

Log in as an administrator into MetaDefender OT Security (<https://<IP> Address>). From the MetaDefender OT Security web administration,

**ClearPass Policy Manager** Integration is accessible under **Integrations > ClearPass Policy Manager Integration** of the **MetaDefender OT Security Site Manager**

After clicking on ‘Enable ClearPass Policy Manager Integration’, the following screen is shown, below is an overview of the ClearPass Policy Manager Integration configuration:

Overview of ClearPass Policy Manager Integration configuration:

### [1. Authentication](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#1-authentication)

All fields are required for the configuration. Use the values collected during ClearPass Policy Manager configuration.

Configuration Authentication

The table below explains the fields used for configuration in detail:

| **Field Name** | **Value/Notes** |
| --- | --- |
| **Server Address** | This should be the ClearPass IP address |
| **Port** | This should be 443 |
| **API Admin Username** | API Administrator User ID created in the previous section |
| **API Admin Password** | API Administrator Password created in the previous section |
| **Client ID** | OAuth2 client ID created in the previous section |
| **Client Secret** | OAuth2 Client Secret copied in the previous section |

### [2. Synchronization](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#2-synchronization)

Configuration Synchronization

#### [2.1. Periodic Sync](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#21-periodic-sync)

Metadefender OT Security can synchronize data with ClearPass Policy Manager using a custom time setting specified by the user, with units in minutes. The default synchronization interval is 5 minutes.

#### [2.2. Automation Sync](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#22-automation-sync)

Metadefender OT Security can synchronize data with ClearPass Policy Manager using a custom trigger sync based on conditions. When you click on 'condition', the following screen is displayed:

Custom trigger sync by conditions

The users can click on the toggle or checkbox to enable or disable conditions.

Metadefender OT Security can automatically synchronize data with ClearPass Policy Manager upon detection of changes in asset properties based on asset types:

Conditions about asset type

Metadefender OT Security can automatically synchronize data with ClearPass Policy Manager upon detection of changes in asset exposure score within or outside the defined range:

Conditions about asset exposure score

#### [2.3. Manual Sync:](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#23-manual-sync)

Metadefender OT Security can synchronize data with ClearPass Policy Manager immediately by clicking the **Sync Now** button

### [3. Test Configuration and Apply](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#3-test-configuration-and-apply)

Once configured, click on **Test Connection**. A message is displayed at the top right corner “**Test successfully**”.

After clicking on the **Apply** button. A message is displayed “**Update ClearPass Policy Manager configuration successfully**”, which indicates the configuration is saved successfully.

The connection status changed to '**Connected**' after the configuration successfully.

## [Integration Results](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#integration-results)

As part of enabling the above integration, MetaDefender OT Security will create several custom Endpoint Dictionary attributes using the ClearPass REST APIs. This is a record of the Dictionary Attributes created by MetaDefender OT Security

Check under **ClearPass Policy Manager** > **Administration > Dictionaries > Dictionary Attributes.**

### [1. Endpoint Dictionary Attributes created by MetaDefender OT Security:](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#1-endpoint-dictionary-attributes-created-by-metadefender-ot-security)

Endpoint Dictionary Attributes created by MetaDefender OT Security

### [2. Example of Endpoints created by MetaDefender OT Security:](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#2-example-of-endpoints-created-by-metadefender-ot-security)

The Endpoint data is sent by MetaDefender OT Security, it creates the Endpoints, sets the endpoint classification, and also configures some custom endpoint attributes. An example of the endpoints created is shown below.

Example of Endpoints created by MetaDefender OT Security:

### [3. Normalized Endpoint data created by MetaDefender OT Security](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#3-normalized-endpoint-data-created-by-metadefender-ot-security)

### [4. Custom Endpoint data created by MetaDefender OT Security](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#4-custom-endpoint-data-created-by-metadefender-ot-security)

In addition to the standard data, MetaDefender OT Security also supplies other custom attributes. Click on the Attributes tab to see them.

Custom Endpoint data created by MetaDefender OT Security

## [Monitoring/Reviewing ClearPass Policy Manager and MetaDefender OT Security communications](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#monitoringreviewing-clearpass-policy-manager-and-metadefender-ot-security-communications)

### [1. On MetaDefender OT Security](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#1-on-metadefender-ot-security)

Once the sync has started endpoint data will be populated directly into the ClearPass Policy Manager endpoint database, view the last update time from the integration configuration screen, see below for an example

Reviewing ‘Last sync time’ to ClearPass Policy Manager

### [2. On ClearPass](/docs/md-ot-security/integrations/md-ot-security-site-manager-and-clearpass-policy-manager#2-on-clearpass)

If the sync is not working or shows an error then it’s likely you’ve missed capturing the information correctly, recheck the data recorded, additionally, you can view the API calls between MetaDefender OT Security and ClearPass Policy Manager from **ClearPass Guest > Administration > Support > Application Log**. Below is an example of logs from MetaDefender OT Security to ClearPass Policy Manager. Filter using the IP address of MetaDefender OT Security.

Example of API logs between MetaDefender OT Security and ClearPass Policy Manager
