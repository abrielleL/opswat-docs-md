<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/management-console -->

# Management Console

The MetaDefender Kiosk Management Console allows you to manage the MetaDefender Kiosk system through a web browser.

## [Supported browsers](/docs/mdkiosk/v4.8.5/operating/management-console#supported-browsers)

- Chrome
- Firefox
- Edge

---

## [Access to the console](/docs/mdkiosk/v4.8.5/operating/management-console#access-to-the-console)

The Management Console can be accessed through `http(s)://<MetaDefender Kiosk system>:8009`. After an initial, fresh installation, a [configuration wizard](/docs/mdkiosk/v4.8.5/installation/configuring-the-management-console-for-initial-use) is displayed to setup the Management Console.

A user must log in to access the management console. The username is case-insensitive. A user can either be local to the management console or from a connected user directory. For local users, a maximum of 5 unsuccessful login attempts are allowed until the management console disallows any further logins for 30 minutes. For users from a user directory, any lock out security is expected to be handled on the user directory side. Once logged in, if no activity is made for some time, the idle user will be automatically logged out.

*Kiosk Console login*

---

## [Access allowed for each role](/docs/mdkiosk/v4.8.5/operating/management-console#access-allowed-for-each-role)

An administrator is allowed to access all features of the Management Console

An auditor is only allowed to view and retrieve logs; no changes can be made to the Kiosk under this role

|  | User role |  |
| --- | --- | --- |
| **Management Console section** | **Administrator** | **Auditor** |
| Dashboard |  |  |
| Configuration |  |  |
| Workflows |  |  |
| Logs |  |  |
| License |  |  |
| Resources |  |  |
| Documentation |  |  |
| Central Management Details |  |  |
| - Disconnect (when managed) |  |  |
| Backup/Restore |  |  |
| Security |  |  |
| Login Settings |  |  |
| - User Directories |  |  |
| - Local Users |  |  |
| - Change Password (*local user only*) |  |  |

---

## [Product Management Enrollment](/docs/mdkiosk/v4.8.5/operating/management-console#product-management-enrollment)

Logging in to the Management Console will display an enrollment dialog menu:

*Product management enrollment*

This is currently an experimental feature phase rollout to allow [enrolling](https://docs.opswat.com/my/product-management/enroll-an-instance) & managing a Kiosk with `My OPSWAT`.

Viewing basic instance inventory and license information will be supported in a future `My OPSWAT` release in September 2023.

Further management capabilities will be rolled out in subsequent releases.

Kiosk will continue to fully support On-Premise Management via Central Management v7 - read [Configuring with Central Management](https://docs.opswat.com/mdkiosk/configuration/configuring-with-central-management) for further guidance.

---

Review [Continue reading](/docs/mdkiosk/v4.8.5/advanced-deployment/additional-kiosk-configuration) for more details on the Management Console and configuration settings.
