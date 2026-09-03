<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-is-kiosk-skipping-files- -->

[MetaDefender Kiosk (Windows)](https://www.opswat.com/docs/mdkiosk)Need Help?
# Why is Kiosk Skipping Files?

View the session history for more details regarding Skipped Files

- Navigate to “Settings” > “Logs” > “Session History”. Here you can click on the “Session ID” for more information.

1. Media scanned contains **encrypted** or **password-protected** files that MetaDefender Core cannot unlock. You can view these under “Files Blocked” for more details, click on the “Blocked” reason to view “File Path”, “Process Server”, “File Type”, “File Name”, “SHA256” hash.

Continue to scroll down for further details

When scanning Media, if Kiosk detects a password-protected file, it will prompt the user to enter the password. If a password is not entered, the file will be skipped.

Kiosk allows you to pre-load passwords into the Kiosk Web Management console and MetaDefender Core Web Management console.

On the MetaDefender Core > Workflow Management > Workflows > “Kiosk” workflow > “Archive” tab, you can select predefined passwords

System files may be locked, if you have “Skip processing locked system files”, these files will be skipped.

2. Scan exceeded archive size or file failed to scan

Under MetaDefender Core > Workflow Management > Kiosk > Archive

- You can select limits for archive files, defining how deep you want to scan the file. If these limits are reached and the file has not been fully scanned yet, this can result in a “skipped file” or “blocked file”. Increase these limits and scan the file again.
- If you have “Handle archive extraction task as failed when” checked, the file may be skipped if the following occur: “Invalid file structure”, “Extracted partially”, “Unsupported compression method”, “general unextractable errors”, “others [archive engine unavailable, disk space issue, system errors, etc.]”. We suggest viewing the file under “Kiosk session log” to view the specific reason for the file.

You can also navigate to MetaDefender Core to view the reason [you can search by session ID to narrow down scan]

MetaDefender Core > Processing History > Processing > Select Kiosk scan

3. Overall File Size is too big

Under MetaDefender Core > Workflow Management > Workflows > Kiosk, you can increase the default file scan sizes.

If you also have file sizes specified on the workflow, you can increase them under MetaDefender Kiosk > Workflows > Select workflow used for scan [Guest or Employee] > Processing > File limits

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
