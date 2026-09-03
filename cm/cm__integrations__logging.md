<!-- source: https://www.opswat.com/docs/cm/integrations/logging -->

# Logging

The add-on for Splunk has INFO log level set by default. However, if a user wants to change this, they can change the Logging level from the Logging tab.

![](https://uploads.developerhub.io/prod/97qW/oun1o4p888vhc60o14de12x3cyfcf8dwgwo8cirda18hwvr12jd8xs67k51hmvtg.png)

Note that logging messages go to Splunk’s internal index and does not count against the Splunk license quota. However, if you would like to ingest the add-on’s log to a custom index, you can copy the snippets below and adding them to the default/inputs.conf configuration file (can be found in C:\Program Files\Splunk\etc\apps\TA-opswat-metaaccess\default\inputs.conf). Ensure that you replace both occurrences of <logging index> with the custom internal logging index you want to use. After adding the custom internal logging snippets to the inputs.conf file, restart Splunk to apply the changes. If at any time you need to disable logging to the custom index, simply update ‘disabled = 0’ to ‘disabled =1’ and restart Splunk.

```plaintext
[monitor:///$SPLUNK_HOME/var/log/splunk/ta_opswat_metaaccess_metaaccess_logs.log]
disabled = 0
index = <logging index>
sourcetype = opswat:ta:logs
 
[monitor:///$SPLUNK_HOME/var/log/splunk/ta_opswat_metaaccess_metaaccess_api.log]
disabled = 0
index = <logging index>
sourcetype = opswat:ta:logs
```

To view the messages logged to the custom internal index, simply enter the Search app and enter the following query

```plaintext
index=<logging index>
```
