<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/is-there-a-performance-sla-for-file-scanning- -->

# Does MetaDefender Cloud include a performance SLA for file scanning?

This article applies to all paid MetaDefender Cloud license holders. For more information on our range of licensing and evaluation options, please [Read This](https://metadefender.opswat.com/licensing).

Yes, for paid license holders, MetaDefender Cloud commits to a performance service-level agreement (SLA) for file scanning.

Response times, which vary per licensing plan, are listed below.

### [**Standard licensing plan:**](/docs/mdcloud/knowledge-base/is-there-a-performance-sla-for-file-scanning-#standard-licensing-plan)

- 8 seconds for Multiscanning and Deep CDR (p50). In this case, p50 means that the median (or middle value) of all scan times across a given month must fall at or under 8 seconds.
- 500 milliseconds for API calls (p50). In this case, p50 means that the median (or middle value) of all API calls across a given month must fall at or under 500 milliseconds.

### [**Professional licensing plan:**](/docs/mdcloud/knowledge-base/is-there-a-performance-sla-for-file-scanning-#professional-licensing-plan)

- 8 seconds for Multiscanning and DeepCDR (p75). In this case, p75 means that 75% of all scan times across a given month must fall at or under 8 seconds.
- 500 milliseconds for API calls (p75). In this case, P75 means that 75% of all API calls across a given month must fall at or under 500 milliseconds.

### [**Enterprise licensing plan:**](/docs/mdcloud/knowledge-base/is-there-a-performance-sla-for-file-scanning-#enterprise-licensing-plan)

- 8 seconds for Multiscanning and Deep CDR (p90). In this case, p90 means that 90% of all scan times across a given month must fall at or under 8 seconds.
- 500 milliseconds for API calls (p90). In this case, p90 means that 90% of all API calls across a given month must fall at or under 500 milliseconds.

Please Note:

When using Multiscanning technologies such as MetaDefender Cloud, it is important to understand that all AV engines have different scan times, even for the same file. Because Multiscanning is performed by all engines in parallel, the total scan time for a given file will reflect the time of the slowest engine in your package.

**Other factors influencing scan time include:**

- File Type

  - Generally, archives take longer, as all files within the archive must be scanned
- File Size

  - A 20kb *pdf* will scan much faster than a 250 mb *.pptx*, for example
- Current Traffic

  - All files are added to where they wait to be picked up and scanned
  - Time spent in the queue influences overall scan time
  - Scan requests from MetaDefender Cloud customers are given priority over free API users in the queue.

Pro Tip:

For faster results, OPSWAT highly recommends that you upgrade to the **Enterprise** license option, as this not only offers higher file size limits, but also highest queue priority for scanning. For more information about **Enterprise** and other license options, [Read This.](https://metadefender.opswat.com/licensing)

Support:

If you are experiencing **Performance Issues That Could Constitute A Breach Of The MetaDefender Cloud Performance SLA**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
