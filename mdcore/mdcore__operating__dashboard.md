<!-- source: https://www.opswat.com/docs/mdcore/operating/dashboard -->

# Dashboard

MetaDefender Core provides a Web-based user interface (default port is 8008) that gives a general overview of MetaDefender Core status and allows you to configure its options.

## [Security page](/docs/mdcore/operating/dashboard#security-page)

The Security page shows information on

#### [Processing Summary](/docs/mdcore/operating/dashboard#processing-summary)

Displays a summary for the selected instance and time range: total files scanned, allowed, blocked, and failed.

#### [Threats Detected](/docs/mdcore/operating/dashboard#threats-detected-)

Displays the top threat verdicts detected and top file-blocking verdicts within the selected time range.

#### [Data Loss Prevented](/docs/mdcore/operating/dashboard#data-loss-prevented)

#### [Number of Sanitized](/docs/mdcore/operating/dashboard#number-of-sanitized)

#### [Security Trend](/docs/mdcore/operating/dashboard#security-trend)

Displays Security Trend charts — threats detected, DLP hits, and sanitized files over time — for the selected range, grouped by hourly, daily, weekly, or monthly time buckets.

#### [Top 5 File Types with Threats Detected](/docs/mdcore/operating/dashboard#top-5-file-types-with-threats-detected)

#### [**Verdicts Blocked Detected**](/docs/mdcore/operating/dashboard#verdicts-blocked-detected)

#### [Top 5 File Types by Verdict](/docs/mdcore/operating/dashboard#top-5-file-types-by-verdict)

#### [**CVE Volume Trend**](/docs/mdcore/operating/dashboard#cve-volume-trend)

Displays CVE detections over time, broken down by severity (Critical, Important, Moderate, Low, or Unknown) for the selected time range and bucket size.

#### [Most Active CVEs](/docs/mdcore/operating/dashboard#most-active-cves)

Displays the most frequently detected CVEs for the selected time range, along with their severity and number of detections

#### [Top 10 Countries Detected](/docs/mdcore/operating/dashboard#top-10-countries-detected)

#### [**Top 10 Vendors Detected**](/docs/mdcore/operating/dashboard#top-10-vendors-detected)

## [System page](/docs/mdcore/operating/dashboard#system-page)

The System page page shows information on

#### [File Submission](/docs/mdcore/operating/dashboard#file-submission)

Displays the number of submitted and blocked files over time for the selected time range, processing rule, and bucket size (hourly, daily, or monthly), counted either per submission or per object

#### [File Processing Time](/docs/mdcore/operating/dashboard#file-processing-time)

Displays the File Processing Time widget, showing how long each engine spent processing files over time (in milliseconds) for the selected time range and bucket size (hourly, daily, or monthly), viewable as an average or total

#### [Reuse Processing Result](/docs/mdcore/operating/dashboard#reuse-processing-result)

#### [Total Objects Scanned](/docs/mdcore/operating/dashboard#total-objects-scanned)

## [Usage page](/docs/mdcore/operating/dashboard#usage-page)

The usage page is to provide the current system resource status (CPU, memory and disk) and processing performance (scan queue) of MetaDefender Core server.

## [Quarantine](/docs/mdcore/operating/dashboard#quarantine)

The Quarantine page shows all scanned files which are copied to the quarantine. Each of them can be pinned to avoid removal on cleaning up. Also comments can be written to each quarantined file. Quarantine log can be searched for comment, file name and source of the scan request.

## [Update history](/docs/mdcore/operating/dashboard#update-history)

The Update history shows information on every update package related event.

On the Update history page you can also search for engine name, package type or message content. Also you can filter the list for severity.

## [Configuration history](/docs/mdcore/operating/dashboard#configuration-history)

The Configuration history shows information on user activity events regarding workflow rule changes, setting changes, engine setting changes, licensing.

You can search for text on the Configuration history page and filter the list for datetime.
