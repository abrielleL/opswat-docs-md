<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/can-i-export-scheduled-scan-reports-via-api-calls-or-email- -->

# Can I export scheduled scan reports via API calls or email?

This article applies to MetaDefender Core versions **5.13.0** and later deployed on Windows and Linux systems.

**Overview:**

MetaDefender Core does not currently support direct scheduled reporting or exporting of processing history via **API calls**.

However, it is possible to set up **scheduled email reports** of processing history.

**Steps to Configure:**

1. **SMTP Configuration:** Configure your SMTP server under Settings > Network > Email server.

   - For more details, refer to [Email configuration](https://www.opswat.com/docs/mdcore/configuration/email-configuration)
2. **Schedule Report Configuration:** Configure the schedule report under Settings > Schedule Report > Processing Activity or Executive Report.

**Verify the Change:**

- After configuration, check that scheduled reports are sent to the configured email address.

**Related Articles:**

- More details on schedule report can be found here: <https://www.opswat.com/docs/mdcore/configuration/schedule-report>

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
