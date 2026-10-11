<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/what-does-each-scanning-engine-status-indicator-mean- -->

# What does each scanning engine status indicator mean?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to the MD Kiosk version 4.7.6 or above

Starting from MD Kiosk version 4.7.6, a new feature has been introduced in the Kiosk UI to display the scanning engine status.

These icons provide a quick and clear overview of the MD Core antivirus engine status. Below are the descriptions of each status icon:

## [1. Status Operational:](/docs/mdkiosk/v4.8.6/knowledge-base/what-does-each-scanning-engine-status-indicator-mean-#1-status-operational)

- MD Core is connected
- Engines are up-to-date and ready to scan

## [2. Status Warning:](/docs/mdkiosk/v4.8.6/knowledge-base/what-does-each-scanning-engine-status-indicator-mean-#2-status-warning)

- 1 or more engines are outdated.
- 1 or more engines are updating
- Engine updating failed

## [3. Status Critical:](/docs/mdkiosk/v4.8.6/knowledge-base/what-does-each-scanning-engine-status-indicator-mean-#3--status-critical)

- MD Core is not connected (connection failed).
- MD Core license has expired.

## [Viewing detailed engine status](/docs/mdkiosk/v4.8.6/knowledge-base/what-does-each-scanning-engine-status-indicator-mean-#viewing-detailed-engine-status)

Starting in MD Kiosk version 4.8.4, you can tap the status icon to see more detail without leaving the Kiosk UI. This opens an **Engine Information** window listing every anti-malware engine currently running on the connected MD Core.

For each engine, the window shows:

- The engine's name and version
- The date its virus definitions were last updated
- A colored indicator — green if the engine is up to date, orange if it's outdated — matching the overall status icon

If no engine information is currently available, the window shows **No engines available** instead of a list. Select **Got it** to close the window and return to the previous screen.

The window updates automatically as engine status changes, so you don't need to close and reopen it to see the latest information.

Note

If your Kiosk is configured to allow updating engines offline from a USB drive, tapping the status icon may also give you access to that update option alongside the detailed engine view. See [Offline update Core engine via Kiosk UI](/docs/mdkiosk/v4.8.6/docs/mdkiosk/advanced-deployment/offline-update-core-engine-via-kiosk-ui) for details on that feature.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
