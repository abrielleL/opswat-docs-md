<!-- source: https://www.opswat.com/docs/ocm/configuration/setting-up-domain -->

# Server URL

The server URL is a URL that you assign to your OPSWAT Central Management. This URL can be configured during the setup wizard for a fresh installation or later at Setting > Server Configuration > Security. However, we recommend that you should configure all security settings at early stage. The Server URL can be a domain, IPv4, or IPv6.

The Server URL will be used to:

- validate settings when you make changes on Server Configuration
- embed into the MetaDefender Endpoint installers and executable files. MetaDefender Endpoint will use that URL and the MetaDefender Endpoint Recovery Key to talk to the OPSWAT Central Management server.
- pass to managed MetaDefender Core instances. MetaDefender Core uses this URL to download engines' update packages.

Warning

Please be advised that changing the Server URL of the OPSWAT Central Management server can cause devices that have installed MetaDefender Endpoint to NOT be able to connect to this server.

This should be done before you distribute MetaDefender Endpoint to your devices to avoid any disruption.

## [Via the setup wizard](/docs/ocm/configuration/setting-up-domain#via-the-setup-wizard)

After a fresh installation, a setup wizard will be loaded to walk you through steps to set up your OPSWAT Central Management server. At the step #3, you can fill in a server URL you would like to set for your OPSWAT Central Management instance.

## [Via the management console](/docs/ocm/configuration/setting-up-domain#via-the-management-console)

The Server URL settings is located at **Settings** > **Server Configuration** > **Security**.
