<!-- source: https://www.opswat.com/docs/mddrive/configuration/managing-drives-with-central-management -->

# Manage MetaDefender Drives with OPSWAT Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

After booting the MetaDefender Drive you intend to connect with My OPSWAT Central Management, go to **Settings → My OPSWAT Central Management**, and check the connection status

Follow the instructions below according to the form factors, to enroll your MetaDefender Drive to OPSWAT Central Management.

- [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive User Interface](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-drive)
- [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive Toolkit](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-toolkit)
- [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive with Smart Touch](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-smart-touch)
- [Enroll MetaDefender Drive to Central Management Server from KIOSK](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-kiosk)

### Update MetaDefender Drive remotely via Central Management

If you are connecting to an OPSWAT Central Management Server 7.8 or later, the following options will be available, for both SaaS and Onprem setups.

- **Update definitions from this OCM:** check this box to allow MetaDefender Drive to fetch engine definition updates from this server
- **Update version from this OCM:** check this box to allow MetaDefender Drive to download and install its software upgrade packages from this server

Administrator can **view and schedule the updates** from Central Management by going to **Platform → Updates → Modules**

### Centrally Manage and control advanced settings of MetaDefender Drives

Administrators can manage these settings directly and centrally from OPSWAT Central Management:

- From version v4.4.10: MetaDefender In-Session Scan Settings. From Smart Touch v2.4.0, Smart Touch applies the Central Management settings again after each scan session, so changes made in In-Session during a session do not carry over to the next one.
- From version v4.4.10: MetaDefender Drive with Smart Touch Certificates (one Kiosk certificate for Secure File Storage, and up to three Wi-Fi CA certificates for enterprise Wi-Fi).

  - To do so, first, navigate to Smart Touch Console area on Central Management
  - Then upload the certificates from there
  - From Smart Touch v2.4.0, a Wi-Fi CA certificate from Central Management can be chosen on Smart Touch when joining a network. See [Configure MetaDefender Drive with Smart Touch](https://www.opswat.com/docs/mddrive/configuration/smart-touch-configurations).
- From Smart Touch v2.4.0: **Smart Touch Passcode**, to set a new passcode on the Drive, for example when the operator forgot it. See [Configure MetaDefender Drive with Smart Touch](https://www.opswat.com/docs/mddrive/configuration/smart-touch-configurations).
- From Smart Touch v2.4.0: **Remote Control**, to wipe Secure File Storage or lock a lost Drive. See [Wipe Data and Lock a Lost Drive with Smart Touch from Central Management](https://www.opswat.com/docs/mddrive/configuration/wipe-and-lock-smart-touch-remotely-from-cm).

### View Device and Admin Events

Administrator can also view the **Management Logs**

1. **Admin Events**, including Engines update
2. **Device Events**
