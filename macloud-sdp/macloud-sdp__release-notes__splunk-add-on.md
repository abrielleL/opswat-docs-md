<!-- source: https://www.opswat.com/docs/macloud-sdp/release-notes/splunk-add-on -->

# Splunk Add-on

**Release History**

## [3.0.0](/docs/macloud-sdp/release-notes/splunk-add-on#300)

Additional features added to this version:

- Upgraded Get Logs API to v3.2 for MetaAccess Logs input
- Added support for additional Event category "Device Report" to MetaAccess Logs input
- Upgraded Get Device Details API to v3.4 for MetaAccess Device Logs input
- Added Device Username in device Vulnerabilities events.
- Separated List of Vulnerabilities for a given device into Separate events to avoid Multi-value field handling for user while writing search query for Vulnerability events.
- Fixed a bug in MetaAccess Device Logs input where in certain situations, the Additional API calls for get Device Details and get CVE keep getting skipped for certain Event Triggers selected by User while creating input.

## [2.0.0](/docs/macloud-sdp/release-notes/splunk-add-on#200)

Additional features added to this version:

- A new input, MetaAccess Device Logs, allows admins to retrieve device event logs as well as device details and device CVEs for certain events such as when the device becomes non-compliant or device has reported issues.

## [1.1.0 - May 03, 2021](/docs/macloud-sdp/release-notes/splunk-add-on#110---may-03-2021)

This is the first version.

Features supported in this release

- Allow an admin configure MetaAccess accounts where the admin would like to collect data from
- Admins can define inputs to collect data from MetaAccess accounts

  - MetaAccess Logs Input: admins can retrieve event logs from an account. This input will retrieve event logs incremental by its interval.
  - MetaAccess API Input: admins can retrieve data such as devices, account information, vulnerabilities from an account. This input will retrieve the current data at the time it runs by its interval
  - Get Admin Logs, Get Device Logs, Get Vulnerabilities, Get Account Details, and Get Devices inputs OOTB
- Admins can configure a log level, and proxy settings
