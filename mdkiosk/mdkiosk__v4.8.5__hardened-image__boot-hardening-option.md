<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/hardened-image/boot-hardening-option -->

# Boot Hardening Option

**Purpose**

This article document shows how to enable “Boot Hardening Option” for MetaDefender Kiosk during system configuration.

Detail benefits when enabling “Boot hardening option” in MD Kiosk

- Prevent unauthorized users from accessing desktop functionalities on PC.
- AD can access to desktop after gracefully close Kiosk applications by Alt+S.

**Solution**

To set up “Boot hardening option” in MD Kiosk, please read through the following guidance for step-by-step instructions.

| Setup Progress | Description |
| --- | --- |
| Step 1 | Access to **Kiosk Web Management Console** |
| Step 2 | Navigate to **Settings**, select **System Hardening** |
| Step 3 | Click "**Enable**" button to activate **Boot Hardening option**.  Enabling boot hardening will cause the system to boot/login to a blank desktop until the Kiosk fully loads. Basic PC functionality will not be available until the Kiosk is gracefully closed. Access to this management console is necessary to disable the boot hardening. |
| Step 5 | Click "**Save Setting**" |

**Support**

If you encounter any problems with this guide or if the steps provided do not work, please contact [OPSWAT Support] (<https://www.opswat.com/support>).
