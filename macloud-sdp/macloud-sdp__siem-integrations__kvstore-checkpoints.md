<!-- source: https://www.opswat.com/docs/macloud-sdp/siem-integrations/kvstore-checkpoints -->

# KVStore Checkpoints

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The application saves important data like script execution timestamps and API authentication tokens to Splunk’s KVStore as “checkpoints”. The checkpoints should not require any maintenance, but if needed, can be found at the following location within Splunk on data collection node(HF).

$Splunk_home/var/lib/splunk/kvstore/mongo/s_TA-ops<random data>
