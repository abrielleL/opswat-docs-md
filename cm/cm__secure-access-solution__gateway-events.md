<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/gateway-events -->

# Gateway Events

To monitor gateway activity, console users are able to review Gateway Session Logs (seen in [SDP Reporting Features](https://docs.opswat.com/macloud-sdp/v3.10.0/secure-access/sdp-reporting-features)) , monitor gateway events though the My OPSWAT Central Management logs, and establish notification groups.

## My OPSWAT Central Management Logs: Gateway Events

The My OPSWAT Central Management Logs can provide time stamped gateway activity. These events can also be sent via email notifications within the Notification Group component of My OPSWAT Central Management. For more information, please review the Notification Group section of this article.

![](https://uploads.developerhub.io/prod/97qW/0hzylzgp6pjgx3b9e7tltygw54257952pd37jkm0y5dgt6xwtzbw0v1iwqfc1wfd.png)

1. Navigate to Logs -> Gateway Events.
2. This page consists of all relevant gateway event logging, but console users can filter it based on specific gateway activity. These filters can be activated by selecting the ‘Filters’ button and checking off the boxes associated with the activity:
   - **Registered** indicates when a gateway is registered.
   - **Rebooted** indicates when a gateway is rebooted.
   - **Connection Lost** indicates when a gateway is no longer able to communicate with the My OPSWAT Central Management backend.
   - **Connection Restored** indicates when a gateway that was down was able to restore communication with the My OPSWAT Central Management backend.
   - **Update Started** indicates when a gateway started the update process.
   - **Update Failed** indicates when a gateway's update process failed.
   - **Update Successful** indicates when a gateway's update process successfully completed.
3. Console users can also use the search bar to search by gateway name or gateway ID.
4. To filter the events based on timeframe, select ‘Timeframe’ and users can set the timeframe to: Today, Yesterday, Last 7 days, Last 30 days, or Custom. *
5. To export these logs (with filers applied), press ‘Export Filtered Events’ and submit your PIN. This will trigger the download of the filtered events as a CSV file.

## Notification Groups: Gateway Events

1. Navigate to Settings -> Notification Groups.
2. In the upper right-hand corner, select “**+ Add Notification Group**”.
3. When selecting ‘Triggers’ for your group to be notified on, you can select:
   - **Gateway Events** are events that trigger a notification regarding the gateways detected on the licensed account. The events under this category are:
     - **Gateway registered**, which indicates when a new gateway is registered to the licensed account
     - **Gateway connection lost**, which indicates when established gateways are unable to communicate with MetaDefender IT Access’ backend.
     - **Gateway restarted**, which indicates when a gateway has been restarted.
     - **Gateway connection restored**, which indicates when a lost gateway connection has been re-established.
     - **Gateway update started** indicates when a gateway started the update process.
     - **Gateway update failed** indicates when a gateway's update process failed.
     - **Gateway update successful** indicates when a gateway's update process successfully completed.

**Custom field can only be set as far back as the account’s ‘Data retention length’. This can be reviewed in Settings -> Global -> Device Data, under Data Retention.*
