<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details -->

# Can't view scan details

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The *View scan details* link on **Dashboard > ICAP history > Request** **details** points to the scan details on the MetaDefender Core instance where the actual scanning took place.

For further details see [4.1. ICAP Dashboard](/docs/mdicap/v5.15.0/operating/icap-dashboard).

## [Symptoms](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#symptoms)

## [Dashboard instead of scan details](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#dashboard-instead-of-scan-details)

The *View scan details* link leads to the **Dashboard** on the referenced Core instead of the scan details.

### [Reason](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#reason)

The *View scan details* link works with MetaDefender Core version 4.7.0 (or later) only.

## [Connection refused or browser is waiting](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#connection-refused-or-browser-is-waiting)

The Web Management Console can not be accessed from the browser. You get an error message (connection refused) or your browser is waiting for reply.

### [Reason](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#reason)

*View scan details* links stop working after the referenced Core is uninstalled or migrated to a new address.

## [Page not found](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#page-not-found)

The browser displays a page not found error, however everything seems to be configured properly.

### [Reason](/docs/mdicap/v5.15.0/troubleshooting/can-t-view-scan-details#reason)

*View scan details* links use the IP addresses configured at the Core inventory. If these IP addresses are not accessible from the machine where the actual browsing happens, then the details page can not be displayed.
