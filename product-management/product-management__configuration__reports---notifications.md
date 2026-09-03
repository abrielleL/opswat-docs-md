<!-- source: https://www.opswat.com/docs/product-management/configuration/reports---notifications -->

# Reports & Notifications

Administrators can configure events/triggers to receive emails from My OPSWAT to stay updates with account activities and critical issues.

Info

If you deploy My OPSWAT On-premises, please make sure that SMTP settings are configured to allow My OPSWAT send out emails.

### [Reports](/docs/product-management/configuration/reports---notifications#reports)

Administrators can configure My OPSWAT to send a MetaDefender Kiosk summary reports for specific instances or the entire account.

The following options are available:

- **Recurrence Pattern:** Minutely/Hourly/Daily/Weekly/Monthly.
- **Recur every:** Select the update frequency depending on the selected recurrence pattern.
- **Email List:** The email addresses will receive email notifications. Each email address must be entered on a separate line.
- **Instances Included:** Select the MetaDefender Kiosk instances that will be included in the reports.

### [Notifications](/docs/product-management/configuration/reports---notifications#notifications)

Administrators can now stay updated with email notification alerts based on specified triggers without logging into the console.

To enable notifications alerts, click the **Enable notification alerts** slider.

The following options are available:

- **Email List:** The email addresses will receive email notifications. Each email address must be entered on a separate line.
- **Triggers:** The events that will trigger alerts. The following events are available with configurable thresholds.

  - **Product detects any <threshold> level and above risks.**
  - **Product health status is <threshold> issues and above.**
  - **My OPSWAT’s storage is less than <threshold> GB.**

    - This trigger is only available for My OPSWAT On-premises.
  - **Product’s free space is less than <threshold> GB.**
