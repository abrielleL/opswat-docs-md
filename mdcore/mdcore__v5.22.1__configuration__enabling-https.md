<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/enabling-https -->

# Enabling HTTPS

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Core supports accessing Web UI and REST interface via HTTPS. This feature is not enabled by default.

There are two ways to enable the feature:

- via Management Console or
- modifying MetaDefender Core server configuration via configuration files.

Info

TLS v1.2 and v1.3 are supported HTTPS connection.

Warning

If HTTPS is configured via both: Web Management console and configuration file, only the settings made on Management Console will take effect. It is highly recommended not to use both configuration files and Management Console for HTTPS settings at the same time.

## [Enabling HTTPS via Management Console](/docs/mdcore/v5.22.1/configuration/enabling-https#enabling-https-via-management-console)

1. Go to **Settings→Security** page

2. If there's no certificate-key pair added to the Library, please go to **Library→**[Certificates](/docs/mdcore/v5.22.1/operating/library-management#certificates) add one that is desired to use for securing HTTP connections.

3. Check ***Enable certificate*** *connection* button and choose a certificate-key pair.
4. Users can define advanced SSL settings in the **"Advanced SSL Settings"** section. These settings follow Nginx syntax.

4. As clicking on *Save changes*, you will be warned that Management Console is going to be restarted and this will take some time.
5. Approximately 30 seconds after confirming saving of configuration the Management Console will be reloaded via HTTPS.

## [Enabling HTTPS via configuration files](/docs/mdcore/v5.22.1/configuration/enabling-https#enabling-https-via-configuration-files)

Info

Starting from version **5.14.0**, advanced SSL settings can be configured directly through the UI. We highly recommend using the UI for SSL configuration to ensure better management and ease of use.

For config HTTPS via configuration file, please use this instruction: [SSL Configurations](/docs/mdcore/v5.22.1/configuration/ssl-configurations)
