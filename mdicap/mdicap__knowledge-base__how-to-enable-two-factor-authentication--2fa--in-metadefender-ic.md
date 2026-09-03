<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-enable-two-factor-authentication--2fa--in-metadefender-ic -->

# How to Enable Two-Factor Authentication (2FA) in MetaDefender ICAP Server?

This article applies to MetaDefender ICAP Server releases deployed on Windows and Linux systems.

### [**Overview**](/docs/mdicap/knowledge-base/how-to-enable-two-factor-authentication--2fa--in-metadefender-ic#overview)

MetaDefender ICAP Server does **not** natively support Two-Factor Authentication (2FA). To enable 2FA, you must integrate MetaDefender ICAP with a Single Sign-On (SSO) solution. The SSO solution will manage 2FA through its identity provider.

### [**Configuration**](/docs/mdicap/knowledge-base/how-to-enable-two-factor-authentication--2fa--in-metadefender-ic#configuration)

Integrate MetaDefender ICAP Server with a Single Sign-On (SSO) solution to enable and manage 2FA.

1. Configure MetaDefender ICAP to work with your chosen SSO provider: [Single Sign-On (SSO) Documentation](https://www.opswat.com/docs/mdicap/configuration/single-sign-on--sso-).
2. Once SSO is configured, enable and manage 2FA settings through your identity provider's administrative interface.

### [**Verify the Change**](/docs/mdicap/knowledge-base/how-to-enable-two-factor-authentication--2fa--in-metadefender-ic#verify-the-change)

- Log in to MetaDefender ICAP using SSO credentials.
- Verify that the 2FA process is correctly initiated and functioning as expected within your identity provider.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
