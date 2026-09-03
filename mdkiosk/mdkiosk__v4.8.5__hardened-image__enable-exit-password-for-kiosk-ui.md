<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/hardened-image/enable-exit-password-for-kiosk-ui -->

# Enable Exit Password for Kiosk UI

### [Purpose](/docs/mdkiosk/v4.8.5/hardened-image/enable-exit-password-for-kiosk-ui#purpose)

The Kiosk UI can be exited using the Alt-F4 keyboard combination. By default, Kiosk UI can be closed without password required. This article document shows how to enable “Exit Password” for Kiosk UI.

Detail benefits when enable “Exit Password” function in MD Kiosk:

- Prevent unauthorized personnels to turn off Kiosk functions on the device.
- Guarantee continuous system operation without disruption.

### [Solution](/docs/mdkiosk/v4.8.5/hardened-image/enable-exit-password-for-kiosk-ui#solution)

To enable “Exit Password” in MD Kiosk, please read through the following guidance for step-by-step instructions

| Setup Progress | Description |
| --- | --- |
| Step 1 | Access to **Kiosk Web Management Console** |
| Step 2 | Navigate to **Configuration**, select **Kiosk UI** |
| Step 3. | Expand **Exit Application** section, **enable exit password**   - Provide a **password** to exit the Kiosk application - Or, use **AD admin credentials** (requires Active Directory configured)   The MetaDefender Kiosk application can be exited using the Alt-F4 keyboard combination. If a exit credentials is required, the user will be prompted to enter the password or credential of AD users assigned as Kiosk Administrators after hitting Alt-F4. |
| Step 4 | Click **Save Updates** |

### [Applying the Exit Password to Restart and Shutdown](/docs/mdkiosk/v4.8.5/hardened-image/enable-exit-password-for-kiosk-ui#applying-the-exit-password-to-restart-and-shutdown)

By default, the exit password (or AD admin credentials, if configured) is also required when choosing **Restart** or **Shutdown** from the Kiosk UI — not just when exiting to the Windows desktop.

If you'd rather let users restart or shut down the Kiosk without entering the exit password, while still requiring it to reach the Windows desktop, you can turn this off:

1. Access the **Kiosk Web Management Console**.
2. Navigate to **Configuration**, select **Kiosk UI**.
3. In the **Exit Application** section, disable the option to require the exit password for Restart and Shutdown.
4. Click **Save Updates**.

With this turned off, users can restart or shut down the device directly from the Kiosk UI without a password prompt. Exiting to the Windows desktop always requires the exit password (or AD admin credentials) when exit password is enabled, regardless of this setting.
