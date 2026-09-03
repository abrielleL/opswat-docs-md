<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/email-configuration -->

# Email Configuration

Users with administrator privilege on MetaDefender Core are allowed to setup email configurations for SMTP in order to enable password recovery feature (please check [Password Recovery](/docs/mdcore/v5.21.0/configuration/password-recovery)).

## [SMTP configuration](/docs/mdcore/v5.21.0/configuration/email-configuration#smtp-configuration)

### [Server configuration](/docs/mdcore/v5.21.0/configuration/email-configuration#server-configuration)

| Properties | Description | Option |
| --- | --- | --- |
| SERVER HOST | SMTP server host | IP address / Domain all accepted |
| SERVER PORT | SMTP server port | Some default common ports:   - 25 (TCP) - 465 (SSL) - 587 (TLS) |
| CONNECTION TYPE | Specify type of connection between MetaDefender Core and SMTP server | - TCP (Unsecured email transmission protocol) - SSL (Secured email transmission protocol) - TLS (Secured email transmission protocol) |
| AUTH METHOD | Specify the authorization protocol connecting to SMTP server | - AUTH PLAIN - AUTH LOGIN (preferred) - NONE (no authentication) |

### [User authentication](/docs/mdcore/v5.21.0/configuration/email-configuration#user-authentication)

| Properties | Description | **Constraint** |
| --- | --- | --- |
| EMAIL | Email address |  |
| USERNAME | Username for SMTP authentication (No required if AUTH METHOD = NONE) | Disallowed characters: [] : | ; = * ? < > / \ " |
| PASSWORD | Password for SMTP authentication (No required if AUTH METHOD = NONE) |  |

Please make sure to hit "SAVE SETTINGS" button once configuration is done.

Otherwise "CLEAR SETTINGS" button once hit will clear up all mail settings on the page.

### [Test Email Server configuration](/docs/mdcore/v5.21.0/configuration/email-configuration#test-email-server-configuration)

Before saving the email server configuration, the users can test the setting via the feature "Send test email"

The test email will look like this

## [Microsoft 365 OAuth](/docs/mdcore/v5.21.0/configuration/email-configuration#microsoft-365-oauth)

### [How to get Client Secret and Client ID](/docs/mdcore/v5.21.0/configuration/email-configuration#how-to-get-client-secret-and-client-id)

1. **If you already have this setup, please ignore those steps and goto step 7 and step 8**
2. **Log in to:** [**Microsoft Azure**](https://portal.azure.com/)
3. **Select Microsoft Azure Entra ID**

4. **Register a new app**

5. **Add Graph APIs**

6. **Give correct permissions for Mail: Mail.ReadWrite and Mail.Send**

7. **Give correct permissions for User: User.Read.All**

8. **Expected result**

9. **Copy client id and tenant id**

10. **Generate client secret (if it does not exist)**
