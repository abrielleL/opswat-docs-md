<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/advanced-deployment/session-logs -->

# Session Logs

## [Viewing Scan Results details](/docs/mdkiosk/v4.8.5/advanced-deployment/session-logs#viewing-scan-results-details)

MetaDefender Kiosk displays the most recent scan results on the Logs page.

You can select any of these sessions to view details from that scanning session.

Similarly, you can click see the details of each file in the list of total files processed.

## [Export Session or File History to CSV](/docs/mdkiosk/v4.8.5/advanced-deployment/session-logs#export-session-or-file-history-to-csv)

The session or file history can be exported, on demand, to a CSV file based on the time range selected. Automated history export can be configured on the [Configuration page](/docs/mdkiosk/v4.8.5/advanced-deployment/configuring-global-kiosk-settings).

To export these scan sessions, the admin can use the **"Export Session History"** feature on the KIOSK Console, as shown in the image below.

Exported session history contains information on *SessionID, User ID, Scan Start Time, Scan End Time, Total Files Scanned, Total Files Processed, Total Files Size, Total Files Skipped, Total Files Allowed, Total Files Blocked, Scanning System, Device ID, Device Type, Device Manufacturer, Device Model, Device Serial Number* *and User Question responses*. Some sessions with secondary destination media will show the second at the next line.

Exported file history contains information on *Session ID, User ID, File Name, SHA-256 hash, Scan Result, Scan Result Description and Scanning System.*

## [Searching by file hash or session ID](/docs/mdkiosk/v4.8.5/advanced-deployment/session-logs#searching-by-file-hash-or-session-id)

You can also search MetaDefender Kiosk logs by either file hash (SHA256) or by MetaDefender Kiosk session ID on the Session History page.

If you search by session ID, MetaDefender Kiosk displays a summary of the results of that session.

## [Searching by specific file name](/docs/mdkiosk/v4.8.5/advanced-deployment/session-logs#searching-by-specific-file-name)

Click **Want to upload a file to search** to upload a file to check if it has been processed by MetaDefender Kiosk.

If you search by SHA256 hash code, MetaDefender Kiosk displays a summary of all of the times that file was processed by MetaDefender Kiosk.
