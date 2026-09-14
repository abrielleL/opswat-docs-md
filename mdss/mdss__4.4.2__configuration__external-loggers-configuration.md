<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/external-loggers-configuration -->

# External Loggers Configuration

This feature allows you to forward event logs from MetaDefender Storage Security to an external system.

This is essential for centralized monitoring, security analysis, and integrating with a SIEM (Security Information and Event Management) platform, such as Splunk.

## [**Supported Platforms and Formats**](/docs/mdss/4.4.2/configuration/external-loggers-configuration#supported-platforms-and-formats)

- **Syslog** uses the UDP protocol and requires the RFC5424 format
- **Kafka** connects directly to an Apache Kafkla cluster.

## [**Before You Begin**](/docs/mdss/4.4.2/configuration/external-loggers-configuration#before-you-begin)

Before adding a configuration, ensure that your external logging server is already deployed and accessible from your MetaDefender Storage Security instance. You will need:

- A Syslog server ready to accept UDP traffic.
- Or, an Apache Kafka cluster with a designated topic.

## [**How to Configure an External Logger**](/docs/mdss/4.4.2/configuration/external-loggers-configuration#how-to-configure-an-external-logger)

1. In the MetaDefender Storage Security interface, go to **Settings** > **External Loggers**.
2. Click the **+ Add new server** button to open the configuration panel.
3. Fill in the required server details, such as the server type, network address (IP or hostname), and port.
4. Enable the configuration using the toggle switch and save your changes.

##
