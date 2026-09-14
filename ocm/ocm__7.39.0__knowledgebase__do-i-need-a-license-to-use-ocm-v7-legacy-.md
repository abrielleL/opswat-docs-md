<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy- -->

# Do I need a license to use OCM v7 Legacy?

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems.

## [Managing Products via OCM Does *Not* Require a License](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#managing-products-via-ocm-does-not-require-a-license)

Using OCM to manage and monitor products like MetaDefender Core, Email Gateway Security, or Kiosk does not require a separate license. A license is only needed in specific cases, such as exceeding the deployment limit for MetaDefender Endpoint or Kiosk L-Series (Linux). See the screenshot below:

## [License Management within OCM](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#license-management-within-ocm)

License activation and deactivation within the OCM v7 interface is only required for the following products:

- **MetaDefender Endpoint**
- **MetaDefender Kiosk L-Series (Linux version)**

To view or manage licenses for these products:

1. Navigate to the **Settings** tab on the left sidebar.
2. Click on **License** from the dropdown menu.
3. Here, you can activate, deactivate, or view license details for the supported products listed above.

## [Managing Licenses for Other OPSWAT Products](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#managing-licenses-for-other-opswat-products)

For all other OPSWAT products, license management must be done from the product’s specific license page, which can be accessed via the sidebar in OPSWAT Central Management. Each product requires handling its license within its own management interface.

### [Managing MetaDefender Kiosk Windows License as an example](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#managing-metadefender-kiosk-windows-license-as-an-example)

1. Go to **Inventory** in the OCM sidebar.
2. Select **MetaDefender Kiosk Windows**.
3. Click **License Information** for the desired instance.

### [Available Actions:](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#available-actions)

- **Remove License**: Deactivates the current license and refreshes the management page.
- **Update License**: Opens the activation dialog for license renewal.

### [Activation Options:](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#activation-options)

#### [**Online Activation**](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#online-activation)

1. Select **Online Activation**.
2. Enter your license key.
3. The page will reload automatically upon successful activation.

#### [**Offline Activation**](/docs/ocm/7.39.0/knowledgebase/do-i-need-a-license-to-use-ocm-v7-legacy-#offline-activation)

1. Select **Offline Activation** to open the offline menu.
2. Go to [my.opswat.com](https://my.opswat.com/) and:

   - Select **Activate New License**.
   - Choose **MetaDefender Kiosk Windows V4.X**.
   - Enter the **Activation Key**, **Deployment ID**, and an optional description.
   - Click **Request Unlock Key**, then download the activation file.
3. Return to OCM, upload the activation file, and click **ACTIVATE**.
4. The page will reload automatically upon success.

Click on the link to the support article for the product license you wish to manage: 🔗 [Managing MetaDefender Core License](https://www.opswat.com/docs/ocm/integrations/managing-metadefender-core-license)

🔗[Managing MetaDefender Kiosk Windows License](https://www.opswat.com/docs/ocm/integrations/managing-metadefender-kiosk-license)

🔗[Managing MetaDefender Email Gateway Security License](https://www.opswat.com/docs/ocm/integrations/managing-metadefender-email-gateway-security-license)

🔗[Managing MetaDefender ICAP Server License](https://www.opswat.com/docs/ocm/integrations/managing-metadefender-icap-server-license)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
