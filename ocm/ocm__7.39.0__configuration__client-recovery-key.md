<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/client-recovery-key -->

# MetaDefender Endpoint Recovery Key

The MetaDefender Endpoint Recovery Key is used to authenticate the MetaDefender Endpoint managed by OPSWAT Central Management. If you reinstall OPSWAT Central Management, you must register the same MetaDefender Endpoint Recovery Key in the configuration wizard.

This key can only be entered in the configuration wizard. You can view the MetaDefender Endpoint Recovery Key at **Setting > Global Settings > Account.**

Warning

Please do not use the same MetaDefender Endpoint Recovery Key for multiple OPSWAT Central Management server. You should save this key for data recovery purpose.

## [Via the setup wizard](/docs/ocm/7.39.0/configuration/client-recovery-key#via-the-setup-wizard)

After a fresh installation, a setup wizard will be loaded to walk you through steps to set up your OPSWAT Central Management server. At step #3, you can leave the MetaDefender Endpoint recovery key as default OR fill in a key that you already have from a previous installation to make sure MetaDefender Endpoint installed on your devices with that key can authenticate with your server.

## [Via the management console](/docs/ocm/7.39.0/configuration/client-recovery-key#via-the-management-console)

The MetaDefender Endpoint Recovery Key is located at **Setting > Global Settings > Account > Account Settings.**
