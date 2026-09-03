<!-- source: https://www.opswat.com/docs/mdtransferguard/configuration/12-managed-file-transfer-streams -->

# Managed File Transfer and Kiosk Streams

A security dongle must be inserted in the server that you want to change, RED or BLUE.

## [Prerequisites](/docs/mdtransferguard/configuration/12-managed-file-transfer-streams#prerequisites)

Before you configure any transfer parameters:

- Ensure Diode X BLUE and RED network addresses are configured.
- Ensure the current license and personality are uploaded.
- If you are integrating the Managed File Transfer Stream with a Kiosk instance, configure Kiosk to work with the built in MetaDefender Core instance on Diode X BLUE. To do so, consult <https://docs.opswat.com/mdkiosk/configuration/configuring-with-metadefender-core>
- Configure Kiosk instance to work with a Managed File Transfer instance. Note that instead of the Managed File Transfer url you should indicate Diode X BLUE IP address, <https://docs.opswat.com/mdkiosk/configuration/configuring-with-metadefender-vault>
- You may need to generate API keys in Managed File Transfer to integrate with Transfer Guard and Kiosk, to do so consult <https://docs.opswat.com/mdvault/configuration/api-keys>

Info

This must be configured on both the BLUE and RED sides. Each of the sides have their own management UI.

## [BLUE Side Configuration](/docs/mdtransferguard/configuration/12-managed-file-transfer-streams#blue-side-configuration)

Go to the management UI and insert user and password to login.

Click the Streams link and then click on the Action button to deploy the Action menu, then select **Add HTTP**.

Complete the following:

- **Channel:** Assign a channel number.

Info

The channel number needs to be the same on both the BLUE and RED sides.

- **Type:** Type of stream being tracked. Unilateral
- **Name:** Name of the stream
- **Protocol:** For a Managed File Transfer Stream, HTTP is preselected.
- **Source Port:** Port number of the source IP.
- **Source Addresses:** IP address(es) in the BLUE zone where the stream will originate. If you are entering more than one address, separate the addresses with a semicolon.
- **Enabled:** checkbox to enable/disable the stream.
- **Max Sessions:** Maximum number of sessions for the stream
- **Encryption (SSL):** select an option in the dropdown list if you want to encrypt the stream.
- **Description:** user-friendly description.

After filling in the fields, click on the Submit button to save configuration.

## [RED Side Configuration](/docs/mdtransferguard/configuration/12-managed-file-transfer-streams#red-side-configuration)

Go to the management UI and type user and password to login.

Click the Streams link and then click on the Action button to deploy the Action menu, then select Add HTTP.

Complete the following:

- **Channel:** assign a channel number.

Info

The channel number needs to be the same on both the BLUE and RED sides.

- **Type:** Type of stream being tracked. Unilateral.
- **Name:** Name of the stream
- **Protocol:** For a Managed File Transfer Stream, HTTP is preselected.
- **Destination Port:** Port number of the destination IP.
- **Destination Address:** IP address in the RED zone where the stream will terminate. You can enter only one address.
- **Enabled:** checkbox to enable/disable the stream.
- **Description:** user-friendly description.

After filling in the fields, click on the **Submit** button to save configuration.

## [Modify a stream](/docs/mdtransferguard/configuration/12-managed-file-transfer-streams#modify-a-stream)

In the Streams section, click on the stream you want to modify and the Edit Stream menu will be displayed. Modify the Stream and Submit changes.
