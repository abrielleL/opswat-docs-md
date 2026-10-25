<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/what-is-the-behavior-of-icap-license-related-email-notifications -->

# What is the Behavior of ICAP License-Related Email Notifications?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP Server releases (Windows and Linux) starting from version v5.8.0 and later.

### [**Behavior Overview**](/docs/mdicap/v5.15.0/knowledge-base/what-is-the-behavior-of-icap-license-related-email-notifications#behavior-overview)

ICAP license-related email notifications are governed by specific configuration settings. The behavior depends on the type of event and the intervals defined in the system.

#### [**ICAP Notifications**](/docs/mdicap/v5.15.0/knowledge-base/what-is-the-behavior-of-icap-license-related-email-notifications#icap-notifications)

- ICAP-related alerts follow the interval configured under: **Settings → Email Notification** This determines how frequently ICAP event notifications are sent.

#### [**License Notifications**](/docs/mdicap/v5.15.0/knowledge-base/what-is-the-behavior-of-icap-license-related-email-notifications#license-notifications)

There are three main scenarios:

1. **License Expired** or **License Lost**

   - Notifications are sent repeatedly based on the **repeat interval** (**Every N mins/hours/days**) configured in the system.

2. **License About to Expire**

   - Two parameters control this behavior:

     - **Before X Days**: Defines how many days before expiration the notification period begins.
     - **Repeat Every N mins/hours/days**: Sets how often reminders are sent during that period.

### [**Example Behavior**](/docs/mdicap/v5.15.0/knowledge-base/what-is-the-behavior-of-icap-license-related-email-notifications#example-behavior)

- License expires in **20 days**.
- Configuration:

  - Start notifications **30 days before expiration**.
  - Repeat every **10 minutes**.
- **Result**: Since the current date is within the 30-day window, the system will send an email **every 10 minutes** until the license expires or the condition changes.

For more information, please refer to [Email Notification - MetaDefender ICAP Server](https://www.opswat.com/docs/mdicap/configuration/email-notification)

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
