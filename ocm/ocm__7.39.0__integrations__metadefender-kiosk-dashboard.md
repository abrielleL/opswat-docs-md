<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard -->

# MetaDefender Kiosk Windows Dashboard

The MetaDefender Kiosk Windows Dashboard provides an overview of status and activities of all managed MetaDefender Kiosk Windows instances. The MetaDefender Kiosk Windows Dashboard is located at **Dashboard > MetaDefender Kiosk** **Windows**.

Info

The MetaDefender Kiosk Windows Dashboard function can optionally integrate with the ELK (Elasticsearch, Logstash, Kibana) technology, which provides additional features as well as improves data collection performance. To configure ELK settings for OPSWAT Central Management, please refer to [Elasticsearch and Logstash server integration setting](/docs/ocm/7.39.0/configuration/elasticsearch-and-logstash-server-integration-setting). To configure ELK settings for MetaDefender Kiosk Windows, please refer to [Changing MetaDefender Kiosk Windows Configuration](/docs/ocm/7.39.0/integrations/changing-metadefender-kiosk-configuration) and the [MetaDefender Kiosk Windows documentation](https://onlinehelp.opswat.com/kiosk/8.7._Logging_Configuration.html) for more details.

Info

In Logstash server settings, the UDP protocol is recommended to have the collected data visualized correctly. If TCP protocol must be selected, please ensure that the OPSWAT Central Management server can properly resolve the hostname of the managed MetaDefender Kiosk Windows instances, e.g., the server and instances are all installed on the same network.

## [Overview tab](/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard#overview-tab)

### [Statistics by a selected time frame](/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard#statistics-by-a-selected-time-frame)

This section visualizes the activities on all managed MetaDefender Kiosk Windows instances in a selected time frame.

You can view statistics of files that all managed MetaDefender Kiosk Windows instances have scanned. The **FILES PROCESSED** chart presents a number of files that have been processed during the selected time frame and instances.

**(Only available with ELK integration)** After each scan, a MetaDefender Kiosk Windows instance sends a syslog message to the configured ELK server and it is displayed in the **SYSLOG FROM INSTANCES** table.

### [Resources section](/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard#resources-section)

A user can view managed MetaDefender Kiosk Windows instances' connection status, license status and resource usage.

Warning

Please note that for MetaDefender Kiosk Windows instances runs a version older than the version 4.5.8, resource usage information is not available (N/A).

### [Export Report function](/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard#export-report-function)

OPSWAT Central Management provides an ability to export the current state of the MetaDefender Kiosk Windows dashboard to a .pdf or .csv file at including all applied filter settings by selecting **Export Report**.

Warning

Please note that some data fields are not available (N/A) in .csv report for MetaDefender Kiosk Windows instances when ELK integration is enabled or the instance is disconnected.

Additional, an administrator can set up a schedule to auto-send MetaDefender Kiosk Windows reports to specific emails in the **Settings > Reports and Notifications > Email Reports > MetaDefender Kiosk** **Windows** **Report** section. The administrator can customize emails to receive reports, frequency, and what instances are included in the reports (all instances or specific instances).

## [Security tab](/docs/ocm/7.39.0/integrations/metadefender-kiosk-dashboard#security-tab)

The **Security** tab displays a list of security incidents reported by the managed MetaDefender Kiosk Windows instances such as possible threats, sensitive data leaks, suspicious files or potential vulnerabilities by a selected time frame.
