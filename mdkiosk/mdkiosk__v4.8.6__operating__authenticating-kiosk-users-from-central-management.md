<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/authenticating-kiosk-users-from-central-management -->

# Authenticating Kiosk Users from Central Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Authenticating Kiosk Users from Central Management](/docs/mdkiosk/v4.8.6/operating/authenticating-kiosk-users-from-central-management#authenticating-kiosk-users-from-central-management)

If your organization manages Kiosk through Central Management (CM10), you can authenticate users through Central Management instead of connecting each Kiosk device directly to Active Directory. In this setup, Central Management looks up the user (by username and password, or by RFID card) on Kiosk's behalf and returns the matching account details, so individual Kiosk devices don't need direct network access to your identity systems.

This also makes it possible to source users from a system other than Active Directory alone — for example, a separate database of card holders — and still resolve those users to the correct workflow. If a scanned card is recognized but doesn't map to a specific Active Directory account, the session can still proceed under a designated default workflow rather than being rejected.

## [Prerequisites](/docs/mdkiosk/v4.8.6/operating/authenticating-kiosk-users-from-central-management#prerequisites)

- The Kiosk device must be enrolled in Central Management (CM10).

Note

Configuration of this authentication path is done from the Central Management side; contact your Central Management administrator to enable and configure this option.

## [See also](/docs/mdkiosk/v4.8.6/operating/authenticating-kiosk-users-from-central-management#see-also)

- [Setup RFID Card for User Authentication](https://www.opswat.com/docs/mdkiosk/advanced-deployment/setup-rfid-card-for-user-authentication) for configuring RFID authentication directly against Active Directory, without Central Management.
