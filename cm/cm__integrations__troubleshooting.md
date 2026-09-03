<!-- source: https://www.opswat.com/docs/cm/integrations/troubleshooting -->

# Troubleshooting

The default Logging level for the add-on is INFO. If the modular inputs are not working as expected, please set the Logging level to DEBUG to retrieve more messages in the internal logs that may help to find where the problem is.

## 1. How to check error logs for MetaDefender IT Access Logs input

From the Search head, run the below search query to check logs reported by the MetaDefender IT Access Logs input. You need to add an additional text filter “ERROR” in the query to check only error messages

```plaintext
index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_logs.log"
```

## 2. How to check error logs for MetaDefender IT Access Device Logs input

From the Search head, run the below search query to check logs reported by the MetaDefender IT Access Device Logs input. You need to add an additional text filter “ERROR” in the query to check only error messages

```plaintext
index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_device_logs.log"
```

## 3. How to check error logs for MetaDefender IT Access API input

From the Search head, run the below search query to check logs reported by the MetaDefender IT Access API input. You need to add an additional text filter “ERROR” in the query to check only error messages:

```plaintext
index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_api.log"
```
