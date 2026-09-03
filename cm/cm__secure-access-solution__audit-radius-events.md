<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/audit-radius-events -->

# Audit RADIUS Events

With this feature, administrators can track and analyze RADIUS events in real-time or retrospectively. These events may include successful or failed authentication attempts, user session start and end times, accounting information, and other important network activity.

![](https://uploads.developerhub.io/prod/6Ad9/3e4ct2chxv3a834hqij0tba8e9daedek4y1tn0qo2u3jnqsfvybviu6953n7sbpm.png)

1. Navigate to **Logs** → **RADIUS Event**
2. This page contains comprehensive RADIUS event logs, allowing console users to filter the information based on specific activities. The available activities are:
   - **Access** indicates when a device is accessing the Network and get the status response from MetaDefender IT Access as: Successful authentication (Accept) or Failed authentication (Reject).
   - **Accounting** indicates when a device is attempting access to the Network recorded in the system.
   - **Granted access** indicates an attempt to accessing the Network and get the status response from MetaDefender IT Access as Successful authentication (Accept)
   - **Rejected access** indicates an attempt to accessing the Network and get the status response from MetaDefender IT Access as Failed authentication (Reject).
3. Console users can also use the search bar to search a record by multiple options (MAC address, Device name, Device ID, Access Profile, Rule).
4. To filter the events based on timeframe, select ‘Timeframe’ and users can set the timeframe to: Today, Yesterday, Last 7 days, Last 30 days, or Custom.
5. To export these logs (with filers applied), press ‘Export Filtered Events’ and submit your PIN. This will trigger the download of the filtered events as a CSV file.
