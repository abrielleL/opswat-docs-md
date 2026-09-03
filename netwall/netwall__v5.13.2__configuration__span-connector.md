<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/configuration/span-connector -->

# SPAN Connector

SPAN Connector allows the user to copy ethernet traffic from a physical port of the MetaDefender Security Gateway (hereinafter Security Gateway) BLUE and replicates it to a designated SPAN port on Security Gateway RED.

### [Security Gateway BLUE](/docs/netwall/v5.13.2/configuration/span-connector#security-gateway-blue)

Important

To configure SPAN Connector, a security dongle should be inserted in the BLUE server.

1. Login into MetaDefender Security Gateway BLUE.
2. Go to SPAN menu (in Connectors section), deploy Action button and select Add SPAN.
3. Type or select values in the following boxes:

   1. **Port:** Dropdown list of the available ports for span connector. A span port can't be used for any other purpose on MetaDefender Security Gateway. A port used by other process (management IP associated, for instance) will not be displayed on the list.
   2. **Description:** Free text box to include a description of the configured SPAN.
   3. **Enabled**: Check/Uncheck this box to enable/disable this SPAN.
4. Click on Submit button.

### [Security Gateway RED](/docs/netwall/v5.13.2/configuration/span-connector#security-gateway-red)

Important

To configure SPAN Connector, a security dongle should be inserted in the RED server.

1. Login into MetaDefender Security Gateway RED.
2. Go to SPAN menu (in Connectors section), deploy Action button and select Add SPAN.
3. Type or select values in the following boxes:

   1. **Port:** Dropdown list of the available ports for span connector. A span port can't be used for any other purpose on MetaDefender Security Gateway. A port used by other process (management IP associated, for instance) will not be displayed on the list.
   2. **Description:** Free text box to include a description of the configured SPAN.
   3. **Enabled**: Check/Uncheck this box to enable/disable this SPAN.
4. Click on Submit button.
