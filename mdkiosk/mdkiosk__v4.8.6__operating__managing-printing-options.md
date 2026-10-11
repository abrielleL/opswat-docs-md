<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/managing-printing-options -->

# Managing Printing Options

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The Printing Policy page lets you determine whether users have the option to print a receipt of their session and if so, what information will be included on the receipt. The printing is enabled/disabled separately for each action Scan/Retrieve/Wipe.

**Note:** MetaDefender Kiosk will use the printer which is set to default on the system. In case the printer prints to PDF files instead of real device, output PDF files are generated in "C:\Users<username>\AppData\Local\OPSWAT\Metadefender Kiosk\PrintToFile“. Users are not able to select location for PDF files because Kiosk is in full screen hardened mode which does not show any other windows.

Kiosk automatically selects printer paper size

Starting with version 4.8.0, Kiosk automatically uses the paper size (label, A5 or A4) configured in the default printer settings.

Kiosk administrators can configure in details what are included/excluded in/from the report.

Notes:

1. Skipped files are

   - Over-sized files (Upload to MFT for process)
   - Locked system files (Current)
   - Files which are unable to send to core by many reasons (failed to open, failed to send to core,....).
2. Blocked files are those reported “blocked” by Metadefender Core
