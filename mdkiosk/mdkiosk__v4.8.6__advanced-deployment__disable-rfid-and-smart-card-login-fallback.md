<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/disable-rfid-and-smart-card-login-fallback -->

# Disable RFID and Smart Card Login Fallback

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When an RFID card or smart card fails to authenticate, MetaDefender Kiosk normally lets the user fall back to signing in with a username and password. Starting in Kiosk 4.8.2, you can turn this fallback off so that a failed card scan ends the session instead of prompting for credentials — useful for security-sensitive deployments where a card is required and no in-session password alternative should be offered.

## [Prerequisites](/docs/mdkiosk/v4.8.6/advanced-deployment/disable-rfid-and-smart-card-login-fallback#prerequisites)

- Kiosk 4.8.2 or later.
- Remote Active Directory configured as the login method for the Employee workflow.
- At least one of **Enable RFID authentication** or **Enable smart card authentication** turned on. The fallback setting only has an effect once a card-based login method is active.

## [Configuring login fallback behavior](/docs/mdkiosk/v4.8.6/advanced-deployment/disable-rfid-and-smart-card-login-fallback#configuring-login-fallback-behavior)

1. In the Kiosk Management Console, go to **Workflows**, then under **Employee Workflow** click **Set Default Login Method**.
2. Select **MetaDefender Kiosk Authentication**, then **Remote Active Directory**, and confirm your Active Directory server is configured.
3. Turn on **Enable RFID authentication**, **Enable smart card authentication**, or both.
4. In the same area, find **Enable Active Directory username and password login** and set it according to your policy:

   - **Checked (default)** — if a card scan fails, the Kiosk offers a **Login with username & password** option so the user can complete the session with AD credentials.
   - **Unchecked** — the **Login with username & password** option is hidden. If a card scan fails, the Kiosk shows an authentication-failed message and ends the session, returning to the Welcome screen.
5. Save your changes.

If both RFID and smart card authentication are turned off, this checkbox has nothing to apply to and is disabled — there's no card-based login path that could fail.

If your Kiosk is enrolled in Central Management, this setting is configured centrally on the Default Login Method page and pushed to enrolled Kiosks; the local Console field is read-only in that case.

## [What end users see](/docs/mdkiosk/v4.8.6/advanced-deployment/disable-rfid-and-smart-card-login-fallback#what-end-users-see)

**With fallback enabled (default):** if a card doesn't scan successfully, a **Login with username & password** option appears so the session can continue with an Active Directory username and password.

**With fallback disabled:** if a card doesn't scan successfully, the Kiosk shows a message that authentication failed and the session has ended, then returns to the Welcome screen. There is no username/password option on this screen — the user needs to try their card again from the beginning.

Note

Turning off the fallback applies to both RFID and smart card login together on a given Kiosk — you can't allow the fallback for one card type but not the other.

## [Example](/docs/mdkiosk/v4.8.6/advanced-deployment/disable-rfid-and-smart-card-login-fallback#example)

A deployment requires every Employee session to start with a badge swipe, with no password fallback allowed:

1. The administrator enables **RFID authentication** and turns **off** **Enable Active Directory username and password login**.
2. An employee swipes a valid badge — the session starts normally.
3. A different employee swipes an unregistered badge — the Kiosk shows the authentication-failed message and returns to the Welcome screen, with no option to type in a username and password.
4. That employee gets their badge registered with IT, and on the next attempt the swipe succeeds.

Note

After upgrading from an earlier Kiosk version, this option keeps the previous behavior (fallback enabled) until an administrator changes it, so existing deployments aren't affected until this is intentionally turned off.
