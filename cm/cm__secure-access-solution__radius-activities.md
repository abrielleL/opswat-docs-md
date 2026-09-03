<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/radius-activities -->

# RADIUS Activities

![](https://uploads.developerhub.io/prod/6Ad9/3kk8i3r3x1hc7tw7d5xx5ova9vjpy6mxbx09v5kujln3mm745knd3ktw9otz1d7r.png)

1. Navigate to **RADIUS NAC** -> Activities
2. This page displays a table of device information relevant to Network access activity:
   - **Status** indicates that the device is connecting or disconnecting from the Network.
   - **Device Name** if the device currently have agent installed, this field will display hostname of the device. Otherwise display as Unknown.
   - **MAC Address** MAC address of the devices.
   - **RADIUS Username** will display MAC address of device joining Network (if Authentication Method is set to MAB - MAC Bypass) or credentials of user (if Authentication Method is set to 802.1x)  .
   - **Applied Access Profile** indicates what Access Profile is being applied to the device accessing Network.
   - **Applied Rule** indicates the specific rule within the access policy that is being enforced for the device accessing the network.
   - **Time** indicates the start time and end time of a device connecting to Network.
   - **Last seen** indicates the last time a device connect to the Network.
   - **Reauthenticate** trigger the system to send a CoA (Change of Authorization)/Disconnect packet, forced the device to complete 802.1x (or MAB) authentication again to reconnect to the network

To filter by status, select the ‘Filters’ button and check off the desired status.

1. Console users can also use the search bar to search by device id, device name, application user, group, or application.
2. To filter the activity based on timeframe, select ‘Timeframe’ and users can set the timeframe to: Last 1 hour, Last 12 hours, Last 24 hours, or Custom. *
3. To export these logs (with filers applied), press ‘Export Filtered Events’ and submit your PIN. This will trigger the download of the filtered events as a CSV file.
