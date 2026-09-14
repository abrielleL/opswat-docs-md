<!-- source: https://www.opswat.com/docs/cm/product-management/audit-admin-events -->

# Audit Admin Events

To monitor administrator-related activities in My OPSWAT Central Management, console users are able to review **Admin Events** within **Logs**:

1. Navigate to **Logs > Admin Events**.
2. This page consists of all relevant admin event logging, but console users can filter it based on specific activity. These filters can be activated by selecting the **Filters** button and checking off the boxes associated with the activity:
   - **Admin Logged On** indicates when an administrator logs on.
   - **Admin Logged Off** indicates when an administrator logs off.
   - **Admin Failed Authentication** indicates when an administrator attempted to sign in with invalid credentials.
   - **Admin Changed Password** indicates when an administrator changed their password.
   - **Configuration Change** indicates when an administrator has made a change in My OPSWAT Central Management in regards to devices (device name, policies, etc.).
   - **Revoke Registration Code** indicates when an administrator has revoked the registration code under **Settings > Account**.
   - **Submit Support Ticket** indicates when an administrator has submitted a support ticket.
   - **Secure Access Configuration Change** indicates when an administrator has made a change in My OPSWAT Central Management in regards to Secure Access (gateways, protected apps, etc.)
   - **Allowed Vulnerabilities** indicates when an administrator moves a vulnerability to the allow-list.
   - **System Log** indicates when My OPSWAT Central Management releases new versions available for download.
3. To filter the events based on timeframe, select **Timeframe** and users can set the timeframe to: Today, Yesterday, Last 7 days, Last 30 days, or Custom. *
4. To export these logs (with filers applied), press **Export Filtered Events** and submit your PIN. This will trigger the download of the filtered events as a CSV file.

Custom field can only be set as far back as the account’s data retention length. This can be reviewed in __**Settings -> Global -> Device Data**, under **Data Retention**.
