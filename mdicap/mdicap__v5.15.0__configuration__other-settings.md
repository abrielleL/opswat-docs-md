<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/other-settings -->

# Other settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Global settings](/docs/mdicap/v5.15.0/configuration/other-settings#global-settings)

Global settings may be configured under **Settings > System -> Global settings**.

The following properties are available for configuration:

1. USE PERSISTENT CONNECTIONS: When this options is enabled the MetaDefender ICAP Server keeps the connections open, so that they can be reused for several requests.
2. ENABLE PERMISSIVE PARSING: by default MetaDefender ICAP Server verifies requests strictly against the syntax specified in RFCs. If this option is enabled, then the parser is more permissive: e.g. space characters will be allowed in request URLs.

## [Data retention](/docs/mdicap/v5.15.0/configuration/other-settings#data-retention)

Data retention settings may be configured under **Settings > System -> Data retention**.

The following properties are available for configuration:

1. ICAP history clean up: ICAP history records under **Dashboard > ICAP** **history** will be retained for the time configured here.

   1. OFF: Switch off automatic clean up.
   2. 1 HOUR .. 12 MONTHS: ICAP history records are automatically deleted after reaching the age specified by the configuration value.
2. Config history clean up: audit records under **Dashboard > Config** **history** will be retained for the time configured here.

   1. OFF: Switch off automatic clean up.
   2. 1 HOUR .. 12 MONTHS: audit records are automatically deleted after reaching the age specified by the configuration value.
