<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface -->

# Using the Kiosk User Interface

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The following sections give an overview of the end user experience in using the MetaDefender Kiosk.

The exact experience will depend on how each MetaDefender Kiosk instance is configured.

## [Launching MetaDefender Kiosk](/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface#launching-metadefender-kiosk)

Warning

Before v4.6.2, MetaDefender Kiosk accepted all of sensitive keystrokes including the combinations that could be abused to gain system control, even by using HID attack platforms. From 4.6.2 moving forwards, those sensitive and vulnerable-to-abuse keystrokes are disabled, and only re-anabled when KIOSK UI application is not running. Generally, only keystrokes really applicable on KIOSK input areas are allowed.

The MetaDefender Kiosk application automatically launches upon system startup. If there is a system malfunction and you restart the system, MetaDefender Kiosk re-initializes upon startup.

After startup, the idle screen is displayed:

If the MetaDefender Kiosk license is expired or invalid, the MetaDefender Kiosk application displays an error and does not allow usage:

## [Adjusting screen brightness](/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface#adjusting-screen-brightness)

Users have the option to directly adjust screen brightness on the KIOSK UI, especially beneficial for setups in dimly lit surroundings or during low battery situations.

The KIOSK offers 5 levels of brightness adjustment. Simply click on the brightness icon to raise or lower the screen brightness.

*Adjusting screen brightness on KIOSK UI*

Limitations

For external monitor:

- The monitor should support DDC/CI ([Command Interface)](https://en.wikipedia.org/wiki/Display_Data_Channel) for proper brightness control.
- Brightness control may not work properly when connected to the monitor via a hub.
### [Viewing Your Account Information](/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface#viewing-your-account-information)

If your organization has configured MetaDefender Kiosk to show account details after sign-in, a person icon appears once you've signed in with your directory account (by username and password, or by badging in with an RFID card linked to your directory account). This icon can appear in the menu bar or in the dropdown menu, depending on how your administrator has set it up.

Tap the icon to open a panel showing your account details — for example, your name, email address, or other information your organization has chosen to display. Tap the icon again to close the panel. If a piece of information isn't available for your account, that row shows **N/A** instead of being left out.

The panel stays available while you continue using the Kiosk (for example, while inserting media or during processing), and it clears automatically when you sign out — the next person to use the Kiosk will never see your information.

Note

This icon only appears after signing in with a directory account. It does not appear if you sign in as a local Kiosk user, or through certain centrally-managed sign-in integrations.

## [Exiting the User Interface](/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface#exiting-the-user-interface)

`Alt+S` is used to exit the UI.

When exiting the UI, it may take a few minutes if Kiosk is in the middle of processing media. It is not recommended to exit the UI while Kiosk is processing media.

It is strongly suggested to set Exit Credentials (either a password or AD administrator credentials) in order to prevent users from accessing the underlying system. If the Kiosk software is experiencing any malfunction, the UI will not be able to exit and close. The system administrator will have to have to reboot the machine and diagnose the services' operation in Safe Mode.

### [When the exit password is configured](/docs/mdkiosk/v4.8.6/operating/using-the-kiosk-user-interface#when-the-exit-password-is-configured)
