<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/additional-tuning -->

# Additional Tuning

Risk of negative performance impact

Given the nature of these performance tuning parameters, changing tunables of the ICAP Server may negatively affect the performance.

Always change parameters with care. Please contact Support if you are unsure.

MetaDefender ICAP Server tunables are available in the following locations:

- [internal] section in the /etc/mdicapsrv/mdicapsrv.conf configuration file in Linux, or
- HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\internal Registry key in Windows.

Note

All tunable parameters are optional. If not specified, then the default values apply.

The following parameters are available for tuning:

| parameter | scale | default value | minimum value | maximum value | description |
| --- | --- | --- | --- | --- | --- |
| polling_sleep | milliseconds | 20 | 0 | 10 0000 | After submitting files for scanning, ICAP server polls Core for the results. ICAP server waits between two polling attempts. This parameter defines for how long ICAP server should wait between polling attempts. Risk of unnecessary overload Setting this parameter to a low value, especially to 0 puts unnecessary overload to the underlying REST interface and Core. |
| polling_retry | count, integer | 0 (disabled) | 0 | 1 000 | Number of retries in case of errors during polling the scan results. Explanation Under heavy load MetaDefender Core may give errors to ICAP Server's polling requests. Enabling retries increase the chance that polling will finally succeed. Turn off retry When set to 0, ICAP Server won't retry in case of a polling error. |
| retry_sleepbase | milliseconds | 3 000 | 0 | 100 000 | Base time for sleeping between retry attempts in case of polling errors. Example If polling_retry is enabled, and this parameter is set to 1 000, then ICAP server will sleep for 1 second before it retries polling for the first time. |
| retry_sleepincr | milliseconds | 2 000 | 0 | 10 000 | Increment time for sleeping between retry attempts in case of polling errors with this value. Example If polling_retry is enabled, retry_sleepbase is set to 1 000, and this value is set to 500, then ICAP Server will sleep for 1.5 seconds between the first and the second polling retry attempt, 2 seconds between the second and third attempt, and so on. |
| failover_failed | boolean | - since ICAP v5.14.1: true - older version: false | N/A | N/A | Whether to do failover to the next Core in row in the Core server profile pool in case of a *Failed* scan result from Core. |
| failover_notscanned | boolean | - since ICAP v5.14.1: true - older version: false | N/A | N/A | Whether to do failover to the next Core in row in the Core server profile pool in case of a *Not Scanned* scan result from Core. |
| istag_frequency | minutely hourly daily | minutely | N/A | N/A | Changing the ISTag can invalidate the cache on the ICAP client side and make the client update its contents to keep them secure. With this option forced updates of the ISTag can be done with the frequency configured here (every minute, every hour or every day). Supported values:   - *minutely*: change the ISTag once every minute at zero second (example: 2020-04-28 09:08:**00**) - *hourly*: change the ISTag once every hour at zero minute, zero second (example: 2020-04-28 09:**00**:**00**) - *daily*: change the ISTag once every day at midnight (example: 2020-04-28 **00**:**00**:**00**)   All values are interpreted in the server's local time. For details about the ISTag see [4.10 ISTag](/docs/mdicap/v5.14.1/operating/istag). |
