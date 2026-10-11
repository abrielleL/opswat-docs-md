<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/what-are-the-steps-to-retrieve-the-service-tag-for-kiosk-hardwar -->

# What are the Steps to Retrieve the Service Tag for Kiosk Hardware?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk hardware models from Dell.

**Method 1:** Physical Check on the Device

1. Location:

   - For **Desktops** → Back, top, or side of the chassis.
   - For **All-in-One Desktops** → Back panel or the bottom of the stand.
2. Label: Look for a label marked "Service Tag" or "Serial Number" (7-character alphanumeric).

**Method 2:** Command Line Method (CMD)

- Press `Win + R` to open the Run dialog.
- Type `cmd` and press Enter.
- In the Command Prompt window, execute the following command:

HtmlCopywmic bios get serialnumber

- The Service Tag will be displayed as the Serial Number.

**Method 3:** Dell SupportAssist Application

- Press the Windows key and type "SupportAssist".
- Open SupportAssist.
- The Service Tag is displayed at the top of the window.

**Method 4:** BIOS/UEFI Settings

- Restart the desktop.
- During boot, press `F2` to enter BIOS or UEFI settings.
- Navigate to System Information → Locate the Service Tag.

Notes:

- Ensure the system is powered on and accessible if using CMD or SupportAssist.
- For physical checks, make sure to inspect all sides of the chassis.
- If the label is missing or unreadable, use Method 2, 3, or 4.

Support:

In the unlikely event that you have followed the instructions above but are **Unable to allow encrypted Microsoft Purview messages in MetaDefender Email Gateway Security**, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
