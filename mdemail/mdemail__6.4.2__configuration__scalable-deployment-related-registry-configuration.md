<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/configuration/scalable-deployment-related-registry-configuration -->

# Scalable deployment related registry configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page Restart required

After modifying the server configuration entries in the Windows Registry, you must restart the Metadefender Email Gateway Security service in order for the changes to take effect.

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\database](/docs/mdemail/6.4.2/configuration/scalable-deployment-related-registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitydatabase)

| **Parameter** | **Default value** | **Type** | **Required** | **Description** |
| --- | --- | --- | --- | --- |
| instance | *computer name* | string | required | This parameter is the name of the Email Gateway Security instance. |
| process_instances | *instance* | multi-string | required | List of instance names that this instance should process emails for.  _Supported values: The listed instance names,  Empty or *: all instances._  *Example, when there are two instances in a deployment instance1 and instance2, then if this value is set to*   - *instance1: only emails for instance1 are processed on this instance,* - *instance1, instance2: emails both for instance1 and instance2 are processed.* |
