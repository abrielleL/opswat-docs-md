<!-- source: https://www.opswat.com/docs/cm/integrations/installation -->

# Installation

This Add-on is supported on all tiers of a distributed Splunk platform deployment and also on standalone Splunk instances. The table below provides a reference for installing the add-on in a distributed Splunk deployment:

| **Splunk instance type** | **Supported** | **Required** | **Comments** |
| ---- | ---- | ---- | ---- |
| Search Heads | Yes | Yes | All the search time extraction rules takes place on Search Heads |
| Indexers | Yes | No | All data parsing will be done on heavy forwarder only. |
| Heavy Forwarders | Yes | Yes | This Add-on supports only heavy forwarder for data collection. |
| Universal Forwarder | No | No | This Add-on contains Python Scripts to make API calls, hence not supported on Universal Forwarder |

You can follow the below steps to install the OPSWAT Add-on for Splunk

1. Download the Add-on from Splunkbase [here](https://splunkbase.splunk.com/app/5530/)
2. Install the Add-on on your Search Heads and Heavy Forwarder of distributed deployment, you can also install it on IDM if you are on Splunk Cloud.
   1. Login to Splunk server and go to “Manage Apps”, select “install app from File” button and upload the bundle downloaded in step 1.
   2. Alternatively, you can also extract the bundle in the backend at $SPLUNK_HOME/etc/apps,*where*$SPLUNK_HOME_is your Splunk installation directory.
3. After installation, restart the Splunk service.

You can find more details on how to install an add-on based on your deployment type below:

- [Single-instance Splunk Enterprise](https://docs.splunk.com/Documentation/AddOns/latest/Overview/Singleserverinstall)
- [Distributed Splunk Enterprise](https://docs.splunk.com/Documentation/AddOns/latest/Overview/Distributedinstall)
- [Splunk Cloud](https://docs.splunk.com/Documentation/AddOns/latest/Overview/SplunkCloudinstall)
