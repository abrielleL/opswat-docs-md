<!-- source: https://www.opswat.com/docs/ocm/integrations/adding-an-existing-metadefender-kiosk-instance -->

# Adding an existing MetaDefender Kiosk Windows instance

The following guideline describes how to add an existing MetaDefender Kiosk Windows instance to OPSWAT Central Management.

1. Go to the **MetaDefender** **Kiosk** **Windows** management page under **Inventory** in the sidebar.

2. Click the **ADD NEW INSTANCE** button in the top right panel.

3. The dialog **Add Instance** will be opened. Select the **Add an existing Instance** button.

4. Fill the proper inputs and click the **TEST CONNECTION** button to check the connection status.

- **Name:** The name you want to assign to the new MetaDefender Kiosk Windows instance

- **API Key:** The API Key of the MetaDefender Kiosk Windows instance to authenticate the request

- **Server Address:** The address of the MetaDefender Kiosk Windows instance

- **Assign instance to set**: The set of MetaDefender Kiosk Windows instance

5. If this instance is already managed by another OPSWAT Central Management, the force takeover instance dialog will show the information and ask you if you want to force takeover this instance to your OPSWAT Central Management. Click FORCE to proceed.

6. The dialog will be closed and the page will be reloaded automatically if the result is successful.

Info

The status of the new instance is **Connected** after fetching its version information successfully.
