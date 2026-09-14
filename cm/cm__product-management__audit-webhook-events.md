<!-- source: https://www.opswat.com/docs/cm/product-management/audit-webhook-events -->

# Audit Webhook Events

To monitor webhook activity, console users are able to review and monitor webhook events though the My OPSWAT Central Management logs, and establish notification groups.

## My OPSWAT Central Management Logs: Webhook Events

The My OPSWAT Central Management Logs can provide time stamped webhook activity. These events can also be sent via email notifications within the Notification Group component of My OPSWAT Central Management. For more information, please review the Notification Group section of this article.

1. Navigate to **Logs > Webhook Events**.
2. This page consists of all relevant gateway event logging, but console users can filter it based on specific webhook activity. These filters can be activated by selecting the ‘Filters’ button and checking off the boxes associated with the activity:
   - **Added** indicates when a device is added .
   - **Deleted** indicates when a device is deleted.
   - **Changed status to compliant** indicates when a device's compliance status has changed to complaint.
   - **Changed status to non-compliant**  indicates when a device's compliance status has changed to non-complaint.
   - **Changed status to exempted**  indicates when a device's compliance status has changed to exempted.
3. Console users can also use the search bar to search by gateway name or gateway ID.
4. To filter the events based on timeframe, select ‘Timeframe’ and users can set the timeframe to: Today, Yesterday, Last 7 days, Last 30 days, or Custom. *
5. To export these logs (with filers applied), press ‘Export Filtered Events’ and submit your PIN. This will trigger the download of the filtered events as a CSV file.
