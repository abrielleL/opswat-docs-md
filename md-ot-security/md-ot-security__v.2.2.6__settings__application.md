<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/settings/application -->

# Application

Application setting is accessible under **Settings > Application.**

## [Integrations](/docs/md-ot-security/v.2.2.6/settings/application#integrations)

- **MetaDefender Industrial Firewall & IPS:**

Users can enable MetaDefender Industrial Firewall & IPS Integration to access the MetaDefender Industrial Firewall & IPS Management. Please refer to the document **Operating →** **MetaDefender Industrial Firewall & IPS** for more details

- **My OPSWAT:**

Version My OPSWAT: `2024.1.1.8225`

MetaDefender OT Security integrates with My OPSWAT to manage the health status, license, and version of MetaDefender OT Security.

1. Users can get an API URL and Registration Code from My OPSWAT: <https://my.opswat.com/>

Navigate to **My Products** On the Product console UI, the users can get the registration code on their My OPSWAT account. This is a unique code My OPSWAT generates for each account.

Registration Code from account’s My OPSWAT.

On My OPSWAT, under **My Product > Unmanaged Products.** Find ***MetaDefender OT Security*** then click *Learn To Enroll The Product* to get the **Registration Code** and **API URL**

2. Under **Settings > Application.**

- Click to enable My OPSWAT Configuration
- Input *API URL*, *Registration Code* on MetaDefender OT Security
- About *The Update Frequency (minutes)* - Default 60 minutes: meaning the time for MetaDefender OT Security to send health status reports to the My OPSWAT.
- Click Test Connection
- Click Save

3. Go to My OPSWAT

After integration, the user can manage the health status, license, and version of the MetaDefender OT Security on My OPSWAT

Operations

If user doesn’t want to monitor unnecessary connection from a specific device, they can add a specific MAC address with specific or multiple ports. And the system will not capture any connection come from that MAC address and ports.

Every device in the network scanned into MetaDefender OT Security will be assigned a default compulsory learning hours. After finished the learning hours, if Anomaly detection mode is not turned on, MetaDefender OT Security will or will not keep learning the device behavior afterward.

MetaDefender OT Security visual effects sometime may cause the machine to use a lot of hardware resources, this may result in the machine operating unstably. User can disable the effects manually or use the performance scan to check if the machine can handle the visual effects.

## [Archive settings](/docs/md-ot-security/v.2.2.6/settings/application#archive-settings)

MetaDefender OT Security will run all the time, so the number of connections will be huge (millions of records). That will make MetaDefender OT Security take time to handle the very old connection that may not need for user anymore. So user can setup the archive connection to automatically remove the old connection.

User can set the days you want to keep the old connection by enable “Auto archive connection”.

For example: If user set the days is 90 and archive hour of day is 12:00. That mean the connection in the last 90 days will be kept at the 12:00 next day and the other that over 90 days will be stored in archive connection list.

User can completely remove the old connection by enable “Auto remove archived connection”.

User can filter the archive connection list with Started time from/to and also by using the filter at the right.

*Note:* Don’t forget to press the Save button for the changes to be applied. In case you are leaving without saving, MetaDefender OT Security will display a reminder pop-up.

## [Reset all data](/docs/md-ot-security/v.2.2.6/settings/application#reset-all-data)

This function will reset all your data (device, connection, policies). Please careful before using it.

You need to setup the wizard again after resetting all data. If you see the login page displays after reset all data, please press Ctrl + R and the wizard page will show.
