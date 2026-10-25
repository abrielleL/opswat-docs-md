<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/email-configuration -->

# Mail Server Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Go to Settings -> Network -> Email Server**

## [Server configuration](/docs/mdicap/v5.15.0/configuration/email-configuration#server-configuration)

| Properties | Description | Option |
| --- | --- | --- |
| SERVER HOST | SMTP server host | IP address / Domain all accepted |
| SERVER PORT | SMTP server port | Some default common ports:   - 25 (TCP) - 465 (SSL) - 587 (TLS) |
| CONNECTION TYPE | Specify type of connection between MetaDefender ICAP Server and SMTP server | - TCP (Unsecured email transmission protocol) - SSL (Secured email transmission protocol) - TLS (Secured email transmission protocol) |
| AUTH METHOD | Specify the authorization protocol connecting to SMTP server | - AUTH PLAIN - AUTH LOGIN (preferred) - NONE (no authentication) |

## [User authentication](/docs/mdicap/v5.15.0/configuration/email-configuration#user-authentication)

| Properties | Description |
| --- | --- |
| EMAIL | Email address |
| USERNAME | Username for SMTP authentication (No required if AUTH METHOD = NONE) |
| PASSWORD | Password for SMTP authentication (No required if AUTH METHOD = NONE) |

Please make sure to hit "SAVE SETTINGS" button once configuration is done.

Otherwise "CLEAR SETTINGS" button once hit will clear up all mail settings on the page.
