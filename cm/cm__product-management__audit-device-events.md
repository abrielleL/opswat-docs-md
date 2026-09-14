<!-- source: https://www.opswat.com/docs/cm/product-management/audit-device-events -->

# Audit Device Events

To monitor device activity related to My OPSWAT Central Management and MetaDefender Endpoint, console users are able to review **Device Events**:

1. Navigate to **Logs** --> **Device Events**
2. This page consists of all relevant device event logging, but console users can filter it based on specific activity. These filters can be activated by selecting the ‘Filters’ button and checking off the boxes associated with the activity:
   - **Added** indicates when a device is added into My OPSWAT Central Management.
   - **Added with a duplicate MAC Address** indicates when a device is added into My OPSWAT Central Management with a MAC address that already exists.
   - **Exempted** indicates when a device is exempted from all checks and will pass all policy checks.
   - **Unexempted** indicates when a device is unexempted and will perform policy checks as expected.
   - **Removed by an administrator** indicates when a device is removed from My OPSWAT Central Management by an administrator.
   - **Uninstalled by a user** indicates when the MetaDefender Endpoint is uninstalled by a user.
   - **Changed status to compliant** indicates when a device goes from non-compliant to compliant.
   - **Changed status to non-compliant** indicates when a device goes from compliant to non-compliant.
   - **Granted access** indicates when a device was granted temporary access to a protected application.
   - **Revoked access** indicates when a device was revoked a temporary access to a protected application.
   - **Deleted by unseen setting** indicates when a device has been deleted from My OPSWAT Central Management due to being unseen for X amount of day(s) or hour(s) set in either the Global settings or Device Group settings.
   - **Fetch log** indicates when a console-user requests to fetch logs for a device.
   - **Scan threats** indicates when a device has performed the 'scan threat' process with a compliance check.
   - **Compliance check** indicates when a console-user requests to run a compliance check on a device.
   - **Changed Agent Version** indicates when the agent version has been upgraded to a newer version.
   - **Changed SDK Version** indicates when the SDK version has been upgraded to a newer version.
   - **Changed SDP Version** indicates when the SDP version has been upgraded to a newer version.
3. Console users can also use the search bar to search by device name or device ID.
4. To filter the events based on timeframe, select ‘Timeframe’ and users can set the timeframe to: Today, Yesterday, Last 7 days, Last 30 days, or Custom. *
5. To export these logs (with filers applied), press ‘Export Filtered Events’ and submit your PIN. This will trigger the download of the filtered events as a CSV file.

In addition to reviewing **Device Events**, console users can also use **Notification Groups** to set up triggered notifications for some device events.

**Custom field can only be set as far back as the account’s ‘Data retention length’. This can be reviewed in Settings -> Global -> Device Data, under Data Retention.*
