<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/watchdog-behavior -->

# Watchdog Behavior

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The watchdog is an additional process that monitors the running processes of the MetaDefender Kiosk. In the case where the Kiosk exits unexpectedly, the watchdog will run a specified action to take.

## [Configure watchdog behavior](/docs/mdkiosk/v4.8.6/advanced-deployment/watchdog-behavior#configure-watchdog-behavior)

| **Action** | **Description** |
| --- | --- |
| Do nothing | No action will be performed, the system will remain on the secure desktop |
| Restart MetaDefender Kiosk | MetaDefender Kiosk will be restarted while the system remains on the secure desktopFor a brief moment, a blank secure desktop will be displayed before the MetaDefender Kiosk starts up again |
| Log out of Windows | The user currently logged into Windows will have their session terminated and be logged outThe system will exit out to the Windows OS login |
| Lock Windows | The user currently logged into Windows will be locked outThe system will exit out to the Windows OS login where the admin must log back into Windows |
| Restart Windows | The Windows system will be rebootedThe system will either return back to the Windows OS login or be logged in to the default Windows user (this is dependent on the system's automatic login settings) |
