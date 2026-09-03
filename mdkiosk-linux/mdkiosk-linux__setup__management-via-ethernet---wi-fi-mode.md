<!-- source: https://www.opswat.com/docs/mdkiosk-linux/setup/management-via-ethernet---wi-fi-mode -->

# Management - Ethernet / Wi-Fi Mode

## [Connecting to My OPSWAT / Central Management](/docs/mdkiosk-linux/setup/management-via-ethernet---wi-fi-mode#connecting-to-my-opswat--central-management)

If Kiosk will have a direct connection to its management server, then configuring the Kiosk network setting is required.

The system's IP address will automatically fill in if networking capabilities are working. If this value is empty, use the gear icon to configure the network connection.

The `Hostname` and `Registration Code` of the management server are required to connect. Their values are found in the specific settings of the management server configured:

- [My OPSWAT](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#my-opswat)
- [Central Management](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#opswat-central-management)

`Kiosk Name` specifies the Kiosk instance name that is displayed in the product inventory list of the management server for identification.

Click the `Connect` button after filling in the required fields to register Kiosk with the management server.

Once connection is made, Kiosk will begin to setup necessary components and send configuration details.

When setup is complete, Kiosk is ready to process media.

Warning

If setup fails at any point, the Kiosk will have to be restarted and re-onboarded to the management server again.
