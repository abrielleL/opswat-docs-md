<!-- source: https://www.opswat.com/docs/mdcloud/operation/time-and-timestamps-in-metadefender-cloud -->

# Time and timestamps in MetaDefender Cloud

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This page explains which clock MetaDefender Cloud uses, how timestamps are shown in the API and in the web interface, and what you need to do on your side to match them with your own logs.

**The clock MetaDefender Cloud uses**

All MetaDefender Cloud systems keep time in Coordinated Universal Time (UTC). OPSWAT’s servers are synchronised to Amazon Time Sync Service provided by AWS in every region, so every timestamp the service records comes from the same reference clock, whichever region processed your request.

**Timestamps in the API**

Every timestamp the MetaDefender Cloud API returns is in UTC, in ISO 8601 format with a “Z” suffix. For example, a scan that started at 11:17 UTC on 17 May 2023 is reported as 2023-05-17T11:17:14.437Z. This applies to all time fields in scan results, scan history and API key information, such as start_time, created_at and updated_at. When you filter your scan history by date, give the start and end dates in the same format.

**Timestamps in the web interface**

On [metadefender.com](http://metadefender.com) the same timestamps are shown converted to the time zone of your browser, so that you read them in your local time. The value you see in the web interface and the value the API returns for the same scan therefore differ by your UTC offset. For example, a scan recorded as 2023-05-17T11:17:14.437Z in the API appears as 13:17 on 17 May 2023 to a user in Bucharest in summer time.

**What you need to do**

Keep the systems that call MetaDefender Cloud synchronised to a reliable time source, for example your own NTP servers or your cloud provider’s time service. This lets you match the timestamps in your logs with the timestamps in your scan history and results when you investigate an event. When you compare the two, use the UTC value from the API, or convert your local timestamps to UTC first.
