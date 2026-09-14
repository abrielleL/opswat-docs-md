<!-- source: https://www.opswat.com/docs/ocm/7.39.0/operating/opswat-client -->

# MetaDefender Endpoint

## [Distribute MetaDefender Endpoint to devices](/docs/ocm/7.39.0/operating/opswat-client#distribute-metadefender-endpoint-to-devices)

MetaDefender Endpoint can be deployed in many different ways. Here are the most common options.

**Install the agent manually on devices**

To install MetaDefender Endpoint **directly** on a device:

1. Log into the management console
2. From **Dashboard > Overview** or **Inventory > Devices,** click **Add** **Devices**.
3. Click **Download MetaDefender Endpoint for distribution**
4. **Download** either the installer or portable client as you wish and install or run the agent on devices.

Info

The download link is shareable. You can send the download link to your users to download installers by themselves.

**Distribute the agent through Active Directory**:

1. Log into the management console
2. From **Dashboard > Overview** or **Inventory > Devices,** click **Add** **Devices**.
3. Click **Download MetaDefender Endpoint for distribution**
4. **Download** the appropriate client (typically the MSI file).
5. Identify or create an accessible network share location.
6. Copy the MSI file to that location**(do not change the file name).**
7. Using Group Policy Manager, create a GPO with appropriate scope, and link it to an OU.
8. Create software installation for Computer Configuration and/or User Configuration. Provide the full UNC path to the .MSI file.
9. Enable and deploy the policy.

Info

More information on how to use Active Directory to distribute MetaDefender Endpoint: Can I use Active Directory to distribute, enforce or audit MetaAccess usage?

**Other common techniques:**

1. Add MetaDefender Endpoint directly to your golden image for new systems.
2. Distribute MetaDefender Endpoint with your software deployment or distribution tool.

Info

More information on how to create a golden image containing MetaDefender Endpoint: Can MetaAccess be distributed using a golden image, cloned VMs or AMIs?

If you have reached the limit of devices that can be monitored by your account (25 devices for free accounts), please contact sales to purchase additional devices.

## [Enable MetaDefender Endpoint's auto-update feature](/docs/ocm/7.39.0/operating/opswat-client#enable-metadefender-endpoints-auto-update-feature)

MetaDefender Endpoint is capable of automatically updating to the latest version hosted on your OPSWAT Central Management server.

To enable this feature, the administrator needs to enable the Client's auto-update feature in the OPSWAT Central Management console:

1. Log into OPSWAT Central Management console.
2. Navigate to **Settings > Global Settings.**
3. On the **Device Clients** tab, check on the **Allow Client to automatically update to the latest version** option as shown in the screenshot below.
4. Click the **Save** button.

Info

Client update duration

After enabling auto-update feature, MetaDefender Endpoint package changes will be updated within 1 hour
