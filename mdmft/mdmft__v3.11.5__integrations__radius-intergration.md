<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/integrations/radius-intergration -->

# RADIUS Integration

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

RADIUS (Remote Authentication Dial In User Service) is a networking protocol that provides centralized authentication and authorization management for users who connect to network services.

## [Configuration](/docs/mdmft/v3.11.5/integrations/radius-intergration#configuration)

Go to "Settings" → "Authentication Sources" → "RADIUS Integration."

On the configuration page, fill out the following information:

- **Server Address :** The network address of the RADIUS server.
- **Port:** The port on which the RADIUS server listens for authentication communication.
- **Secret:** The secret value required for RADIUS communication. This must match the value configured on the RADIUS server.
- **Timeout:** The communication with RADIUS is stateless and uses UDP. The timeout value in seconds represents how long to wait for a response from the RADIUS server before closing a request as failed.
- **Authentication Protocol:** The authentication protocol to use when requesting authentication from the RADIUS server.

Info

MetaDefender Managed File Transfer supports the following authentication protocols:

- **PAP:** Password Authentication Protocol: Least secure as it sends passwords in plain text. *Not recommended.*
- **CHAP:** Challenge-Handshake Authentication Protocol: More secure than PAP.
- **MSCHAP:** Similar to CHAP, but with a different hashing algorithm.
- **EAP:** Extended Authentication Protocol, including **EAP-MD5** (CHAP over EAP).
Warning

CHAP (Challenge Handshake Authentication Protocol) requires Active Directory to have **reversible encryption** enabled for the user's password. Without this, CHAP authentication will fail with Reason-Code 19, even if the account is otherwise properly configured.

## [Authentication](/docs/mdmft/v3.11.5/integrations/radius-intergration#authentication)

On the "MetaDefender Managed File Transfer™" authentication screen, RADIUS will be available once the administrator sets up the connection to the RADIUS instance. When a RADIUS user authenticates for the first time, a *new local user* will be automatically created with the corresponding username and assigned the *User role*.

Warning

When updating MetaDefender Managed File Transfer, RADIUS is not automatically added to the global *Trusted Network* *setting*. This step has to be performed manually by the Administrator. See [Trusted Network List](/docs/mdmft/v3.11.5/configuration/trusted-network-list) for further details.

## [MFA](/docs/mdmft/v3.11.5/integrations/radius-intergration#mfa)

If MFA is set up on the RADIUS server MetaDefender Managed File Transfer™ will prompt the user to input the challenge code. As soon as the proper challenge code is typed the user will be logged in
