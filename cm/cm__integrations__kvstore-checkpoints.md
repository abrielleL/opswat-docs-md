<!-- source: https://www.opswat.com/docs/cm/integrations/kvstore-checkpoints -->

# KVStore Checkpoints

The application saves important data like script execution timestamps and API authentication tokens to Splunk’s KVStore as “checkpoints”. The checkpoints should not require any maintenance, but if needed, can be found at the following location within Splunk on data collection node(HF).

```plaintext
$Splunk_home/var/lib/splunk/kvstore/mongo/s_TA-ops<random data>
```
