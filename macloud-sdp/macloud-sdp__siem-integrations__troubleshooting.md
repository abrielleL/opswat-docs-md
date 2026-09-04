<!-- source: https://www.opswat.com/docs/macloud-sdp/siem-integrations/troubleshooting -->

# Troubleshooting

The default Logging level for the add-on is INFO. If the modular inputs are not working as expected, please set the Logging level to DEBUG to retrieve more messages in the internal logs that may help to find where the problem is.

## [1. How to check error logs for MetaDefender IT-OT Access Logs input](/docs/macloud-sdp/siem-integrations/troubleshooting#1-how-to-check-error-logs-for-metadefender-it-ot-access-logs-input)

From the Search head, run the below search query to check logs reported by the MetaDefender IT-OT Access Logs input. You need to add an additional text filter “ERROR” in the query to check only error messages

index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_logs.log"
## [2. How to check error logs for MetaDefender IT-OT Access Device Logs input](/docs/macloud-sdp/siem-integrations/troubleshooting#2-how-to-check-error-logs-for-metadefender-it-ot-access-device-logs-input)

From the Search head, run the below search query to check logs reported by the MetaDefender IT-OT Access Device Logs input. You need to add an additional text filter “ERROR” in the query to check only error messages

index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_device_logs.log"
## [3. How to check error logs for MetaDefender IT-OT Access API input](/docs/macloud-sdp/siem-integrations/troubleshooting#3-how-to-check-error-logs-for-metadefender-it-ot-access-api-input)

From the Search head, run the below search query to check logs reported by the MetaDefender IT-OT Access API input. You need to add an additional text filter “ERROR” in the query to check only error messages:

index=_internal source="/opt/splunk/var/log/splunk/ta_opswat_metaaccess_metaaccess_api.log"
