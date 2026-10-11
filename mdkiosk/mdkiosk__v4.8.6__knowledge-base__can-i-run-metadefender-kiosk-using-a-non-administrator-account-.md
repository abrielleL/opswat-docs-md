<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/can-i-run-metadefender-kiosk-using-a-non-administrator-account- -->

# Can I run MetaDefender Kiosk using a non-administrator account?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting Kiosk version 4.8.3, the Kiosk touch UI launches and runs under a standard (non-administrator) Windows account with no elevation prompt, the same as it does under an administrator account. This lets you avoid granting local administrator rights to the account that runs the Kiosk session day to day.

Administrator rights are still required for:

- **Installing MetaDefender Kiosk** and configuring most settings in the Kiosk Web Management Console.
- **A small number of actions that need administrator rights to complete**, such as unlocking a Flash Security encrypted USB device. To keep these actions working when Kiosk is running under a standard account, an administrator can designate a Windows administrator account for Kiosk to use for this purpose, from **Settings > Security**, under **Administrator Privileges Required**. If this isn't configured, a standard-user session that hits one of these actions will see a message explaining that administrator privileges are required and to contact an administrator.

Note

Unlocking a Flash Security device using a designated administrator account currently only works for Kiosk sessions on the local machine. It does not work over a remote session, even when the account is configured correctly.

For general host-hardening recommendations, see the [MetaDefender Kiosk Documentation](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening).
