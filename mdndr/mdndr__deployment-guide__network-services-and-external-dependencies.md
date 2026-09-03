<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/network-services-and-external-dependencies -->

# Network Services and External Dependencies

- **DNS**: Sensors and Manager use DNS for domain resolution. Examples include threat intel lookups, cloud update endpoints, and reverse lookups. Configure primary/secondary servers in the Manager UI.
- **NTP**: All components synchronize time through NTP servers for accurate event timestamps and correlation. Use multiple NTP servers with stratum preference. Configure NTP in the Manager UI.
- **SMTP**: Manager uses configurable external SMTP (TLS/STARTTLS) for alert notifications and reports.
- **Cloud connectivity**: Manager polls OPSWAT cloud hourly (HTTPS) for `sigpack`, `feedpack` (C2/TI/OSINT), and code updates. Manual upload fallback uses MyOPSWAT portal download and application through the Manager UI.
