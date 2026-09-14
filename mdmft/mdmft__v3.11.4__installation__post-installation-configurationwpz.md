<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz -->

# Automated Setup Wizard - Post-Installation Configuration

Summarize Page    Connect to Cursor Connect to VS Code

Post-installation configuration optimizes system functionality by allowing administrators to customize settings, configure security, and establish integrations.

Info

It is only possible to attempt the initial configuration via the ignition files until the setup wizard is not completed.

## [Ignition File](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#ignition-file)

In deployment environments requiring full automation the initial configurations required to start using MetaDefender Managed File Transfer™ may also be completed with relying an ignition file without using the setup wizard.

The ignition file is a JSON file which should be named `spark.json` and is to be placed into the MetaDefender Managed File Transfer™ installation directory.

## [Key Features of the Ignition Process](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#key-features-of-the-ignition-process)

- Resume Work: In case of interruption it may be attempted again starting from where the previous attempt left off.
- Optional Steps: Steps are optional similar to the Setup Wizard.

## [Known Limitations](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#known-limitations)

- May only be attempted once each REST service startup.
- The ignition file must be placed to the MetaDefender Managed File Transfer™ installation directory by the user.
- The ignition file must be removed by the user in case it is not needed anymore.
- The encryption key cannot be saved from the MetaDefender Managed File Transfer™ UI during the ignition process.
- Requesting a trial license is not possible.

## [Feature Overview](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#feature-overview)

- First Admin Account (Mandatory)
- License Activation (Optional)
- SMTP / Microsoft Graph API Configuration (Optional)
- Server / HTTPS Configuration (Optional)

#### [First Admin Account](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#first-admin-account)

The only mandatory section, where you have to create the primary an administrator account.

An example configuration for the default administrator account can be seen on the following snippet.

Admin accountCopy{
"activation_key": null,
"licence_path": null,
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": null,
"smtp_settings": null,
"graph_settings": null
}
#### [License Activation](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#license-activation)

An optional section to activate your MetaDefender Managed File Transfer™ license. Options include:

- Online: Activate your license key through Internet
- Offline: Activate the product via a license file

If both are specified the online method will take precedence.

An example configuration for the online activation can be seen on the following snippet.

Online activationCopy{
"activation_key": "My-Very-Own-Activation-Key,
"licence_path": null,
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": null,
"smtp_settings": null,
"graph_settings": null
}

An example configuration for the oflline activation can be seen on the following snippet.

Offline activationCopy{
"activation_key": null,
"licence_path": "C:/path/to/license.yml",
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": null,
"smtp_settings": null,
"graph_settings": null
}Info

The offline license can be downloaded from the [www.myopswat.com](https://www.myopswat.com) portal. To download an offline license, you must provide the MFT’s deployment ID. This ID can be obtained by accessing the following endpoint on the MFT server: <http://localhost:8010/vault_rest/deploymentid>

#### [SMTP / Microsoft Graph API Configuration](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#smtp--microsoft-graph-api-configuration)

Optional sections to integrate with your SMTP server / Microsoft Graph API to receive email notifications. Only one may be specified at a given time. Specifying both sections will result in no operation being performed.

An example configuration for SMTP can be seen on the following snippet. Please note that the password must be specified in a base64 encoded format.

SMTPCopy{
"activation_key": null,
"licence_path": null,
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": null,
"smtp_settings": {
"host": "localhost",
"port": "2525",
"enableSsl": true,
"ignoreCertificate": true,
"userName": "user",
"domain": "domain.com",
"isEnabled": true,
"password": "eW91cm9uZWFuZG9ubHlzdXBlcnVuaXF1ZXZlcnlzZWN1cmVwYXNzd29yZA==",
"timeout": "30"
},
"graph_settings": null
}

An example configuration for Microsoft Graph API can be seen on the following snippet.

Microsoft Graph APICopy{
"activation_key": null,
"licence_path": null,
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": null,
"smtp_settings": null,
"graph_settings": {
"address_to_use": "spark.admin@opswat.com",
"is_enabled": false,
"client_id": "my-awesome-client-id",
"client_secret": "my~awesome~client~secret",
"tenant_id": "my-awesome-tenant-id",
"use_html": true
}
}
#### [Server / HTTPS Configuration](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#server--https-configuration)

Info

If either server or HTTPS configuration has changed, then the webserver will be restarted.

Optional section to set up webserver details like host, port, and rate-limiting; and use an SSL certificate to enable secure HTTPS communication.

An example configuration can be seen on the following snippet.

Security SettingsCopy{
"activation_key": null,
"licence_path": null,
"default_administrator": {
"user_name": "admin",
"password": "TheOneAndOnlyVerySecurePasswordForAllUseCases",
"email": "spark.admin@opswat.com",
"first_name": "Admin",
"last_name": "Admin"
},
"security_settings": {
"is_enabled": true,
"rate_limit_settings": {
"is_rate_limit_enabled": true,
"shared_memory_size": 10,
"rate": 10,
"burst_size": 20,
"no_delay": false
},
"certificate_path": "C:/path/to/cert.pem",
"key_path": "C:/path/to/key.pem",
"password_path": "C:/path/to/password.txt",
"host": "mft.host",
"port": 443,
"redirect_settings": {
"is_enabled": true,
"port": 80
},
"tls_1_0": false,
"tls_1_1": false,
"tls_1_2": true,
"tls_1_3": true
},
"smtp_settings": null,
"graph_settings": null
}
## [Outcomes](/docs/mdmft/v3.11.4/installation/post-installation-configurationwpz#outcomes)

- Error: In case the configuration couldn't be applied it will be reattempted from the last successful step on the next REST service startup.
- Success: The application is ready to be used.
