<!-- source: https://www.opswat.com/docs/ocm/integrations/metadefender-core-dashboard -->

# MetaDefender Core Dashboard

View as Markdown Ask ChatGPT about this page Ask Claude about this page

OPSWAT Central Management's MetaDefender Core Dashboard gives a general overview of the status and activities of all managed MetaDefender Core instances.

Warning

The MetaDefender Core Dashboard feature is only compatible with MetaDefender Core instances of version 4.18+. Because of the integration with ELK technology, the MetaDefender Core Dashboard function requires users to [configure ELK settings on both OPSWAT Central Management](/docs/ocm/configuration/elasticsearch-and-logstash-server-integration-setting) and [the managed MetaDefender Core instances](https://onlinehelp.opswat.com/corev4/3.2.1.__Startup_Core_Configuration.html).

Warning

In Logstash server settings, UDP protocol is recommended to have the collected data visualized correctly. If TCP protocol must be selected, please ensure that the OPSWAT Central Management server can properly resolve the addresses of the managed MetaDefender Core instances, e.g., the server and instances are all installed on the same network. Setting MetaDefender Core's syslog level to above **info** (such as debug) can cause the connected Logstash server to crash.

If you have not yet configured ELK settings, MetaDefender Core Dashboard will show the message **No log server connected. Please setup a centralized log server at ELK settings** . Click on the link to set up ELK for OPSWAT Central Management.

After the Elasticsearch and Logstash servers are successfully configured and at least one MetaDefender Core instance with correct Logstash server configuration is connected, the MetaDefender Core Dashboard will be displayed properly.

## [Processing Overview](/docs/ocm/integrations/metadefender-core-dashboard#processing-overview)

Processing Overview shows the combined objects processing history of the managed MetaDefender Core instances. The line chart shows the number of objects processed or blocked by date. The donut chart breaks down the block reasons for the object blocked. The bar chart break downs the object blocked or processed by file types. Miscellaneous statistics are also listed such as the number of objects with sensitive data found with MetaDefender Core's Proactive DLP function or the number of threats sanitized by MetaDefender Core's CDR function. The result can be further refined via the **Filter** function, which can be set to show the last 24 hours, the last 7 days or the last 30 days. Users can also set the refresh interval or perform a manual refresh via the **Refresh** buttons.

Info

Objects refers to the files processed by MetaDefender Core instances, including child files contained in a parent archive-type file.

## [Instances](/docs/ocm/integrations/metadefender-core-dashboard#instances)

The Instances section shows the MetaDefender Core instances under management. Each instance is listed with its license status and scan queue.

## [Configuration of data collection frequency](/docs/ocm/integrations/metadefender-core-dashboard#configuration-of-data-collection-frequency)

The data collection frequency for the MetaDefender Core dashboard can be configured in a configuration file located at:

- On Windows systems, ProgramData\OPSWAT\Central\gears-onpremise_definition.properties
- On RedHat and Ubuntu systems, /etc/opt/ocm/gears-onpremise_definition.properties

#Scheduler interval setting (milliseconds)
schedule.core.statistic.interval=60000
schedule.core.scanQueue.interval=60000
schedule.core.processing.history.interval=3600000
