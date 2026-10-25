<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/email-notification -->

# Email Notification

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting from MetaDefender ICAP Server v5.8.0, email notifications are supported. Administrator can enable this feature to receive alerts via email.

**Required Condition:** An email server must be set up. Refer to the [Mail Server Configuration](/docs/mdicap/v5.15.0/configuration/email-configuration) documentation.

## [License](/docs/mdicap/v5.15.0/configuration/email-notification#license)

From v5.8.0 and onwards, these three settings are available for License email notifications:

- License is expired
- License is about to expire
- License is lost

Find setting at **Settings -> Email Notification**

## [Server Profiles](/docs/mdicap/v5.15.0/configuration/email-notification#server-profiles)

From v5.9.0 and onwards, email notifications can be sent when:

- A scan server becomes unreachable
- Server profiles are unavailable in health check settings

## [Disk Space](/docs/mdicap/v5.15.0/configuration/email-notification#disk-space)

From v5.9.0 and onwards, notifications can be disk space reaches the configured threshold.

## [System Resources](/docs/mdicap/v5.15.0/configuration/email-notification#system-resources)

Starting from v5.10.0, email alerts can be configured for to monitor CPU usage and memory (RAM) usage.

## [Certificates](/docs/mdicap/v5.15.0/configuration/email-notification#certificates)

Starting from v5.10.0, email notifications can be configured when a certificate has expired, or is about to expire.

## [Scanned Requests](/docs/mdicap/v5.15.0/configuration/email-notification#scanned-requests)

Starting from v5.10.0, Email alerts can be configured for blocked scan requests. Options include:

- Sending notifications for **all blocked requests** to a defined recipient list.
- Sending notifications for **blocked requests for specific application(s)**, filtered by one or multiple providing options:

  - Host IP/Domain (supports wildcard input)
  - Request URL (supports wildcard input)
  - Client IP (supports wildcard input)
  - ICAP Client IP (supports wildcard input)
