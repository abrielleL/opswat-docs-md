<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/icap-dashboard -->

# ICAP Dashboard

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender ICAP Server's Dashboard gives overview of ICAP Server status.

Note that the default refresh rate of displayed information is 1 minute by default.

## [Overview page](/docs/mdicap/v5.15.0/operating/icap-dashboard#overview-page)

The Overview page shows information on

- Number of blocked requests
- Number of processed requests
- License information
- Number of processed requests chart

Clicking the Settings icon the following properties can be customized:

- Refresh rate (default: 1 minute)
- Time-span displayed (default: 24 hours)

## [ICAP history](/docs/mdicap/v5.15.0/operating/icap-dashboard#icap-history)

The ICAP history shows information on ICAP events in the system.

On the ICAP history page you can search for ACTION, RESULT, HTTP URI, CLIENT IP, PROXY IP, HOST, CORE RULE or ICAP RULE. Also you can filter the list by ACTION.

Note

Due to usability reasons the ICAP history list is not updated automatically. Click the Refresh icon to update.

Info

The RESULT value Undisclosed means that MetaDefender Core did not return a scan result for this entry.

The reason for this value appearing in ICAP History is that MetaDefender Core is configured to provide OVERALL RESULTS ONLY for VISIBILITY OF SCAN RESULTS in the security rule that matches ICAP file scans.

### [Request details](/docs/mdicap/v5.15.0/operating/icap-dashboard#request-details)

Clicking an ICAP history entry displays public details (that do not require authentication on MetaDefender Core) about the scan.

The *View scan details* link points to the scan details on the MetaDefender Core instance where the actual scanning took place.

Note

The *View scan details* link works with MetaDefender Core version 4.7.0 (or later) only.

For MetaDefender Core versions earlier than 4.7.0 the Dashboard is opened.

Info

To generate the *View scan details* links, MetaDefender ICAP Server stores the actual Core IP where the current request's files were scanned.

As a result the *View scan details* links continue to work properly even after a new Core is configured instead the old one.

Note

*View scan details* links stop working after the referenced Core is uninstalled or migrated to a new address.

## [Export to CSV](/docs/mdicap/v5.15.0/operating/icap-dashboard#export-to-csv)

Clicking the EXPORT TO CSV button will export the history list (according to the actual filter conditions) to a CSV file.

Info

The currently active filter conditions apply to the exported list.

All filtered data gets exported, even if the list expands to multiple pages.

Info

The CSV file is written into a HTTP stream, so it gets downloaded by the browser immediately, automatically.

The CSV file is named according to the following scheme:

Naming convention

`icaphistory-<yyyy>-<MM>-<dd>-<HH>-<mm>-<ss>.csv`

For example, if the export happened on 22nd January, 2020; at 12:38:36 PM:

Naming example

`icaphistory-2020-01-22-12-38-36.csv`

Info

The following data is exported for each entry:

<dd>0</dd>

The history above exports to the following CSV:

## [Config history](/docs/mdicap/v5.15.0/operating/icap-dashboard#config-history)

The Config history shows information on configuration changes made via the Web Management Console.

Note

Changes made directly in the configuration file are not reflected here.

On the Config history page you can search for USER, TYPE, CHANGE TYPE, PARAMETER, OLD VALUE or NEW VALUE. Also you can filter the list by DATE.

Note

Due to usability reasons the Config history list is not updated automatically. Click the Refresh icon to update.
