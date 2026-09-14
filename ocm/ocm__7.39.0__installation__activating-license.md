<!-- source: https://www.opswat.com/docs/ocm/7.39.0/installation/activating-license -->

# Activating OPSWAT Central Management license

To activate a product license for OPSWAT Central Management:

1. Navigate to Settings > License in the sidebar menu.

2. Click the **ACTIVATE** button corresponding to a product you desire to open the activation dialog where you can choose an activation option. Note that the screenshot demonstrates here is for the MetaDefender Endpoint product

Please ensure you activate the correct product

OPSWAT Central Management manages licenses for both MetaDefender Endpoint and MetaDefender Kiosk Linux. To activate a license, click the "Activate" button corresponding to the product of your choice. If you encounter a license activation error, double-check that you have selected the appropriate button for your product.

- **Online Activation**: The OPSWAT Central Management server (OCM) will contact the OPSWAT License portal to activate a license for a selected product based on your **Activation Key** and the OCM's **Deployment ID**.
- **Offline Activation:** You can manually activate your activation key for your OCM server on [My OPSWAT](https://my.opswat.com/portal/products) then upload a license file to your server.

For a successful activation, a valid activation key is required regardless of what option is chosen.

### [Online Activation](/docs/ocm/7.39.0/installation/activating-license#online-activation)

To activate the product with this option, the below requirements must be met:

- The server has an Internet connection and can connect to OPSWAT License portal (<https://activation.dl.opswat.com/>)
- You have a valid activation key for OPSWAT Central Management

With Internet connection, OPSWAT Central Management can be activated directly using the **Activation key** received upon purchasing the product. Perform the following steps for an online activation:

1. In the **Activation** dialog, choose Online Activation.

2. Fill the **Activation Key** field with your key.
3. Fill the "**Describe This Deployment"** text box.
4. Click the **ACTIVATE** button to activate.

If your license is valid, the product shall be activated with number of devices/instances limit as you purchased. Otherwise, you will get an error message.

### [Offline Activation](/docs/ocm/7.39.0/installation/activating-license#offline-activation)

You can activate a license with this option if you have the valid **Deployment ID** of the OPSWAT Central Management instance and the **Activation Key** received upon purchasing the product or a trial key.

Please follow the steps detailed below to acquire the activation file containing the unlock key required for offline activation.

1. Log into [My OPSWAT](https://my.opswat.com/portal/products).
2. Click Activate License in the left sidebar menu.

3. In the pop-up dialog, select the corresponding product for the **Product** field.

   - MetaDefender Endpoint for OPSWAT Central Management v7
   - MetaDefender Kiosk L-Series

4. Enter your activation key and your OPSWAT Central Management's deployment ID
5. Click the Activate button.
6. Click **Download** in the next dialog to download the activation file.

7. Go back to the OPSWAT Central Management console and lick the **ACTIVATE** button corresponding to a product you desire to open the activation dialog.

Please ensure you activate the correct product

OPSWAT Central Management manages the licenses for both MetaDefender Endpoint and MetaDefender Kiosk Linux. To activate a license, click the "Activate" button corresponding to the product of your choice. If you encounter a license activation error, double-check that you have selected the appropriate button for your product.

8. Select Offline Activation option
9. Click **Choose file** to browse for the activation file and click the **ACTIVATE** button.

Info

If you have activated your server, but your license then becomes invalid or expired, an error message will be shown on the console.
