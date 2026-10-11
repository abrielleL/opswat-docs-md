<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-retrieving-the-kiosk-file-history-not-working-for-sessions-w -->

# Why retrieving the Kiosk file history not working for sessions with a large number of files?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Issue](/docs/mdkiosk/v4.8.6/knowledge-base/why-retrieving-the-kiosk-file-history-not-working-for-sessions-w#issue)

When exporting the Kiosk file history, the process seems to take an excessive amount of time and is never completed.

## [Cause](/docs/mdkiosk/v4.8.6/knowledge-base/why-retrieving-the-kiosk-file-history-not-working-for-sessions-w#cause)

This issue occurs because Nginx has a default 3-minute wait period for the report to be generated. If the report includes sessions with a large number of processed files, it may exceed this time limit, leading to a timeout.

## [Solution](/docs/mdkiosk/v4.8.6/knowledge-base/why-retrieving-the-kiosk-file-history-not-working-for-sessions-w#solution)

To resolve this issue, increase the `proxy_read_timeout` setting in the Nginx configuration file.

**Steps to Modify the Nginx Configuration:**

1. Locate the dynamic.conf file. By default, it is located at: C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client\REST\conf\dynamic.conf
2. Open the file in a text editor with administrative privileges.
3. Increase the proxy_read_timeout value to a higher duration, such as 1200 seconds (20 minutes) or more, depending on your requirements.

### [**Example Configuration:**](/docs/mdkiosk/v4.8.6/knowledge-base/why-retrieving-the-kiosk-file-history-not-working-for-sessions-w#example-configuration)

4. Save the changes and restart the MetaDefender Kiosk service for the new settings to take effect.

After increasing the timeout, exporting the file history should be completed successfully even for large reports.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
