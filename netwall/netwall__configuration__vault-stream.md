<!-- source: https://www.opswat.com/docs/netwall/configuration/vault-stream -->

# Managed File Transfer and Kiosk

You need a security dongle inserted in the server which configuration you want to change, RED or BLUE.

## [Prerequisites](/docs/netwall/configuration/vault-stream#prerequisites)

Before you configure any transfer parameters:

- Ensure NetWall BLUE and NetWall RED network addresses are configured.
- Ensure the current license and personality are uploaded.
- Configure Kiosk instance to work with a Managed File Transfer instance. Notice that instead of Managed File Transfer URL you should indicate NetWall BLUE IP address, <https://docs.opswat.com/mdkiosk/configuration/configuring-with-metadefender-vault>
- You may need to generate API keys in Managed File Transfer to integrate with NetWall and Kiosk, to do so consult <https://docs.opswat.com/mdvault/configuration/api-keys>

Important

This should be configured in both sides BLUE and RED. Each of the sides have their own management UI.

## [Security Gateway BLUE](/docs/netwall/configuration/vault-stream#security-gateway-blue)

Go to the management UI and insert user and password to login.

Click the Streams link and then click on the Action button to deploy the Action menu, then select Add HTTP.

Complete the following:

- Channel: You have to choose one channel number.

Important

This channel number needs to be the same in the RED side.

- Type: Type of stream being tracked. Unilateral or Bilateral
- Name: Name of the stream
- Protocol: For a Managed File Transfer Stream, HTTP is preselected.
- Source port: Port number of the source IP.
- Source addresses: IP address(es) in the BLUE zone where the stream will originate. If you are entering more than one address, separate the addresses with a semicolon.
- Enabled: checkbox to enable/disable the stream.
- Max Sessions: Maximum number of sessions for the stream
- Encryption (SSL): select an option in the dropdown list if you want to encrypt the stream.
- Description: user-friendly description.

After filling in the fields, click on the Submit button to save configuration.

## [Security Gateway RED](/docs/netwall/configuration/vault-stream#security-gateway-red)

Go to the management UI and insert user and password to login.

Click the Streams link and then click on the Action button to deploy the Action menu, then select Add HTTP.

Complete the following:

- Channel: You have to choose one channel number.

Important

**This channel number needs to be the same in the BLUE side.**

- Type: Type of stream being tracked. Unilateral or Bilateral
- Name: Name of the stream
- Protocol: For a Managed File Transfer Stream, HTTP is preselected.
- Destination port: Port number of the destination IP.
- Destination address: IP address in the RED zone where the stream will terminate. You can enter only one address.
- Enabled: checkbox to enable/disable the stream.
- Description: user-friendly description.

After filling in the fields, click on the Submit button to save configuration.

## [Modify a Stream](/docs/netwall/configuration/vault-stream#modify-a-stream)

In the Streams section, click on the stream you want to modify and the Edit Stream menu will be displayed. Modify the Stream and Submit changes.
