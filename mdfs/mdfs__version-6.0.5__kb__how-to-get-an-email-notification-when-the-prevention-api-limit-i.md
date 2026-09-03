<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/kb/how-to-get-an-email-notification-when-the-prevention-api-limit-i -->

# How to get an email notification when the Prevention API limit is reached in MetaDefender for Salesforce (MDFS)?

## [Overview](/docs/mdfs/version-6.0.5/kb/how-to-get-an-email-notification-when-the-prevention-api-limit-i#overview)

When using MetaDefender for Salesforce (MDFS), file scanning relies on an API key from **OPSWAT MetaDefender Cloud**. Each API key comes with a daily quota based on the customer’s license.

*For example, if a customer purchases a quota of 1,000 Prevention API calls per day, that quota will reset every 24 hours from the time of the first scan of the day.*

- *If the environment scans around 700 files per day, the usage stays within quota.*
- *If more than 1,000 files are submitted in a day, additional files will exceed the quota and will not be scanned.*

To help administrators manage this, MDFS provides **Rate Limit Warning Notifications**, which can be sent by email and/or app alert.

## [How to Enable Prevention API Limit Notifications](/docs/mdfs/version-6.0.5/kb/how-to-get-an-email-notification-when-the-prevention-api-limit-i#how-to-enable-prevention-api-limit-notifications)

To configure email or app alerts for API quota usage:

1. Log in to **MetaDefender Cloud** as an administrator (<https://metadefender.opswat.com/>)
2. Navigate to **MetaDefender Cloud Settings**.
3. Locate the option **Prevention API: Reached % of Limit**.
4. Enable the checkbox to activate the alert.
5. Configure the percentage threshold (e.g., 80%) at which notifications should be sent.
6. Save the changes.

**Example Notification**: When the quota threshold is reached, administrators will receive an email like this:

By enabling the **Prevention API: Reached % of Limit** setting in **MetaDefender Cloud Settings**, administrators can receive automatic notifications when usage approaches or reaches the daily API limit. This gives admins the chance to take action, such as reducing uploads, scheduling scans, or contacting OPSWAT Support before file scans start failing.

Support:

If further assistance is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
