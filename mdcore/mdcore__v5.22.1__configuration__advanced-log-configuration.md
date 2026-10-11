<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/advanced-log-configuration -->

# Advanced Log Configurations

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Since Metadefender Core (MD Core) v5.15.1, we’ve supported advanced log configuration, you can configure the log settings directly through the MetaDefender Core UI, via My OPSWAT Central Management or via API endpoints: [Logging configuration](/docs/mdcore/v5.22.1/metadefender-core#putlogfileconfig)

### [General settings](/docs/mdcore/v5.22.1/configuration/advanced-log-configuration#general-settings)

### [Log file settings](/docs/mdcore/v5.22.1/configuration/advanced-log-configuration#log-file-settings)

Warning

Changing the log file path is not supported when MetaDefender Core is running in a **container environment**.

When importing a MetaDefender Core configuration into a containerized instance, the log file path setting is not applied — only the log level is imported.

### [Syslog settings](/docs/mdcore/v5.22.1/configuration/advanced-log-configuration#syslog-settings)
