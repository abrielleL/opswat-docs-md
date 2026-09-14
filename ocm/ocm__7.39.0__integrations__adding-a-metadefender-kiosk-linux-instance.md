<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/adding-a-metadefender-kiosk-linux-instance -->

# Adding a MetaDefender Kiosk Linux instance

The following guideline describes how to add a MetaDefender Kiosk Linux instance to OPSWAT Central Management.

Info

[A MetaDefender Kiosk Linux license](/docs/ocm/7.39.0/installation/activating-license)  must be activated for the OPSWAT Central Management server.

1. In the MetaDefender Kiosk Linux instance's user interface, navigate to **Network Configuration**. Fill in the required fields.

- **Hostname:** The server URL of the OPSWAT Central Management server. The Server URL can be found in **Settings > Server Configuration > DEVICE API** under **Server URL.**

- **Registration code:** The integration secret of the OPSWAT Central Management server. The registration code can be found in **Settings > Global Settings > ACCOUNT** under **Registration Code .**

2. Select **Connect.** If successful, the MetaDefender Kiosk Linux should then show up in the OPSWAT Central Management console.

Info

The status of the MetaDefender Kiosk Linux instance changes to **Connected** once its version information is successfully fetched.
