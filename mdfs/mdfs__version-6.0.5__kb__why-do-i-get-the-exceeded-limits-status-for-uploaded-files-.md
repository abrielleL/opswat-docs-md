<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/kb/why-do-i-get-the-exceeded-limits-status-for-uploaded-files- -->

# Why do I get the Exceeded Limits status for uploaded files?

## [Overview](/docs/mdfs/version-6.0.5/kb/why-do-i-get-the-exceeded-limits-status-for-uploaded-files-#overview)

As a Salesforce administrator, you can view OPSWAT – MetaDefender Logs to monitor the status of files uploaded to your Salesforce environment. The **Status** column in these logs will indicate whether a file is safe (*No Threat Detected*), infected, or in another state such as *Exceeded Limits*.

This article explains what *Exceeded Limits* means, why it occurs, and how to check your API limit usage.

## [What *Exceeded Limits* Means](/docs/mdfs/version-6.0.5/kb/why-do-i-get-the-exceeded-limits-status-for-uploaded-files-#what-exceeded-limits-means)

When you click into a specific log entry with the *Exceeded Limits* status, the **MD Scan Details** section will display a message similar to:

Info

Rate limit exceeded, retry after the limit is reset. The limit will be reset in XX hours YY minutes ZZ seconds.

This means your purchased API quota for scanning files in MetaDefender Cloud has been fully used. Once the daily limit is reached, MetaDefender Cloud will no longer accept new file scans until the quota resets.

### [Why It Happens](/docs/mdfs/version-6.0.5/kb/why-do-i-get-the-exceeded-limits-status-for-uploaded-files-#why-it-happens)

- MetaDefender Cloud uses specific APIs (such as **prevention_api**) for scanning.
- Each API has a daily quota based on your license.
- When the quota is exhausted, any new file uploads will receive the *Exceeded Limits* status.
- Quotas reset daily, starting from the time of your first scan.

## [How to Check Your API Limits](/docs/mdfs/version-6.0.5/kb/why-do-i-get-the-exceeded-limits-status-for-uploaded-files-#how-to-check-your-api-limits)

**In the MetaDefender for Salesforce Dashboard**

1. Go to your **MetaDefender Log Reports** dashboard in Salesforce.
2. Check the **Limit** table (bottom-right section).
3. Locate the **prevention_api** row.
4. If the **Remaining value** is `0`, your API quota has been reached.

**Via REST API** You can also check your remaining limits programmatically using the MetaDefender Cloud API: [MetaDefender Cloud API – Get API Key Remaining Limits](https://www.opswat.com/docs/mdcloud/metadefender-cloud-api-v4#getapikey-remaining-limits)

JSON response:

JsonCopy{
"reputation_api": 1000,
"threat_intel_search_api": 25,
"prevention_api": 0,
"download_file": 100,
"sandbox_api": 5,
"feed_api": 1000,
"throttling_limit": 500
}

If the value of`"prevention_api"` is 0, your API quota has been reached.

*Note: Consider upgrading your license or purchasing a higher API quota if you frequently hit the limit.*

Info

If further assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
