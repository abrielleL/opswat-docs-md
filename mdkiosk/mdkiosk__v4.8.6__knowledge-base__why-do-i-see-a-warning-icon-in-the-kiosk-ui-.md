<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-do-i-see-a-warning-icon-in-the-kiosk-ui- -->

# Why do I see a warning icon in the Kiosk UI?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Summary

A warning (exclamation mark) or critical (cross) icon may appear in the Kiosk UI when an engine encounters issues. In this case, the issue is related to the Threat Intelligence engine, which is present but not functional due to an older MD Core version.

Symptoms

- Warning icon (exclamation mark) displayed in Kiosk UI
- Application logs show engine-related issues
- Threat Intelligence engine appears as downloaded but not initialized

Example Logs

[8652] [INFO] [Feb 10, 16:32:56:546] UtilFuncs.cpp#2368 logEngineIssues(): {No session} Connected to http://localhost:8008. Issued engines found: Threat Intelligence - State: downloaded;

Cause

The Threat Intelligence engine was introduced starting with MD Core version 5.17.1.

If the system is running an older MD Core version:

- The engine may still be downloaded
- However, it cannot be initialized or used
- The Kiosk detects this mismatch and raises a warning

Behavior by Version

MD Core v5.16 (or older)

- Threat Intelligence engine: Downloaded but not functional
- Kiosk UI: Warning icon displayed
- Application logs: Show engine in "downloaded" state

MD Core v5.17.1 or newer

- Threat Intelligence engine: Fully deployed and functional
- Kiosk UI: No warning displayed
- Logs: No engine-related issues

Resolution

Upgrade the MD Core to version 5.17.1 or later.

Steps

1. Download the latest MD Core version (≥ 5.17.1)
2. Perform the upgrade according to standard procedures
3. Restart the Kiosk application if required
4. Verify:

- No warning icon is displayed
- Threat Intelligence engine is properly initialized

Support: 

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
