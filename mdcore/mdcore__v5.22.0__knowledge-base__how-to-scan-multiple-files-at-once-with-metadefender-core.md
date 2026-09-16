<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-scan-multiple-files-at-once-with-metadefender-core -->

# How to scan multiple files at once with MetaDefender Core

By default, using MetaDefender Core on its own will allow scanning only one file at a time. We do offer the option to manually submit files for scanning, but this does not support folders or multiple files at once.

To achieve the later ( i.e. scanning an external drive, for example), there are multiple ways:

1. Using [MetaDefender Kiosk](https://www.opswat.com/docs/mdkiosk/operating/processing-disk-image-files) in integration with MetaDefender Core
2. Using [MetaDefender Endpoint](https://www.opswat.com/docs/mdendpoint/endpoint-management/malware-multi-scanning-features-on-metadefender-endpoint#malware-scanning-feature-on-metadefender-endpoint) in integration with MetaDefender Core
3. Custom scripting: A custom-made application that browses through a directory, automatically sending files one-by-one for scanning to MetaDefender Core

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
