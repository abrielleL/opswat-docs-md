<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-can-i-reduce-the-load-on-metadefender-core-when-metadefender -->

# How can I reduce the load on MetaDefender Core when MetaDefender ICAP is sending a lot of traffic?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In some cases when there is a lot of traffic being processed through MetaDefender ICAP you can see increases in processing time due to the heavy load and processing requirement on MetaDefender Core. To reduce this load, we have put in place a mechanism to control how often MetaDefender ICAP polls MetaDefender Core for processing results. This does not impact how the traffic is sent to be processed, it only affects the mechanism that retrieves the scan results once a scan completes. This is especially useful when scanning larger files that take long to be processed, where increasing the polling interval can significantly improve performance.

To control the interval of polling as well as how many times a failed poll is retried, you can modify the MetaDefender ICAP configuration according to the operating system on which it is installed:

- `[internal]` section in the `/etc/mdicapsrv/mdicapsrv.conf` configuration file in Linux, or
- `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\internal` Registry key in Windows.

The attributes that can be modified are as follows:

polling_sleep

- Controls the delay between requests sent to MetaDefender Core to check if a processing result is available
- It is defined in milliseconds, with a default value of 20 and a maximum of 10000 (10 seconds)

polling_retry

- Controls how many times a failed poll will be retried before failing
- Is defined as an integer, by default the value is 0 (disabled) and the maximum is 1000

**NOTE**: We recommend changing these values conservatively, as too large changes could potentially lead to unexpected issues.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
